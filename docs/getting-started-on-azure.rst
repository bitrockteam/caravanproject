Getting started on Azure
########################

Requirements
~~~~~~~~~~~~~

Caveat
^^^^^^

Due to the complexity of Azure Resource Manager and Azure Active
Directory roles, you need to be: - Owner of a Subscription - and at least
Application Administrator in AD.

If you would like to try CSI Volumes, you might need to
perform some operations as Global administrator. These steps are
executed via CLI or Azure Portal abd you might need to ask you Azure Administrator
to perform them.

Clone repos
^^^^^^^^^^^

.. code:: shell

   mkdir ~/caravan
   cd ~/caravan
   git clone git@github.com:bitrockteam/caravan-baking.git
   git clone git@github.com:bitrockteam/caravan-infra-azure.git
   git clone git@github.com:bitrockteam/caravan-platform.git
   git clone git@github.com:bitrockteam/caravan-application-support.git

Install and configure Azure CLI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Refer to `Microsoft
Docs <https://docs.microsoft.com/en-us/cli/azure/install-azure-cli>`__
for instructions.

The configured account must have Contributor level access to an Azure
Subscription and Application Administrator in the Active Directory
tenant. We require the existence of a resource group containing a public
DNS zone.

Build VM images
~~~~~~~~~~~~~~~

.. code:: shell

   cd ~/caravan/caravan-baking/terraform

   cat <<EOF > azure.tfvars
   build_on_azure              = true
   build_image_name            = "caravan-centos-image"
   azure_subscription_id       = "YOUR-SUBSCRIPTION-ID"
   azure_target_resource_group = "YOUR-RESOURCE-GROUP"
   azure_client_id             = "YOUR-AZURE-CLIENT-ID"
   azure_client_secret         = "YOUR-AZURE-CLIENT-SECRET"
   EOF

   terraform apply -var-file azure.tfvars

Note: if you need, you can create an Azure Service Principal for running
Packer in the next section.

Build infrastructure
~~~~~~~~~~~~~~~~~~~~

.. code:: shell

   # SUBSCRIPTION_ID where to create resources
   # PARENT_RESOURCE_GROUP shared DNS 
   # LOCATION where to create resources
   # PREFIX prepended to all resources name 

   cd ~/caravan/caravan-infra-azure
   ./project-setup.sh SUBSCRIPTION_ID PARENT_RESOURCE_GROUP LOCATION PREFIX

This will create ``azure.tfvars`` and ``backend.tf`` in the current
directory. You can further edit ``azure.tvars`` with the needed changes.
For example, you might be interested in setting ``use_le_staging=true``
to use for Let’s Encrypt staging endpoint and avoid being rate limited 
if you are going to run certificates request too often initially.

The two helper scripts ``run.sh`` and ``destroy.sh`` can be used to
fully automate the provisioning and destroying of the entire stack,
providing a one-click experience.

To start the provisioning run:

.. code:: shell

   ./run.sh

or

.. code:: shell

   terraform init -reconfigure -upgrade
   terraform apply -var-file azure.tfvars

If you would like to try CSI, see the content of ``zzz_vault_ad_app``
Terraform output.

Configure the platform
~~~~~~~~~~~~~~~~~~~~~~

.. code:: shell

   cd ~/caravan/caravan-platform
   mv PREFIX-backend.tf.bak backend.tf # replace with your prefix
   terraform init -upgrade -reconfigure
   export VAULT_ADDR=https://vault.PREFIX.EXTERNAL_DOMAIN # replace with your configs
   export VAULT_TOKEN=$(cat ~/caravan/caravan-infra-azure/.PREFIX-root_token)
   export NOMAD_TOKEN=$(vault read -tls-skip-verify -format=json nomad/creds/token-manager | jq -r .data.secret_id)
   terraform apply -var-file PREFIX-azure.tfvars # replace with your prefix

Deploy platform applications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: shell

   cd ~/caravan/caravan-application-support
   # repeat as per caravan-platform

Teardown
~~~~~~~~

Destroy resources in all projects via
``terraform destroy -var-file azure.tfvars``

Alternatively you can use ``destroy.sh`` to automate the entire process.

Delete the created resource group and service principal

.. code:: shell

   # SUBSCRIPTION_ID where to create resources
   # PREFIX prepended to all resources name 

   cd ~/caravan/caravan-infra-azure
   ./project-cleanup.sh SUBSCRIPTION_ID PREFIX
