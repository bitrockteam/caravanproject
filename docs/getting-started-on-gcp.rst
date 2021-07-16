Getting started on GCP
######################

Prerequisites
~~~~~~~~~~~~~

Clone repos
^^^^^^^^^^^

.. code:: shell

   mkdir ~/caravan
   cd ~/caravan
   git clone git@github.com:bitrockteam/caravan-baking.git
   git clone git@github.com:bitrockteam/caravan-infra-gcp.git
   git clone git@github.com:bitrockteam/caravan-platform.git
   git clone git@github.com:bitrockteam/caravan-application-support.git

Install and configure Google Cloud CLI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Please refer to `Google Cloud
documentation <https://cloud.google.com/sdk/docs/install>`__ for
installing and configuring Google Cloud CLI.

Build VM images
~~~~~~~~~~~~~~~

.. code:: shell

   cd ~/caravan/caravan-baking/terraform

   cat <<EOF > gcp.tfvars
   build_on_google             = true
   build_image_name            = "caravan-centos-image"
   google_project_id           = "YOUR-PROJECT-ID"
   google_account_file         = "YOUR-JSON-KEY"
   google_network_name         = "caravan-gcp-vpc"
   google_subnetwork_name      = "caravan-gcp-subnet"
   EOF

   terraform apply -var-file gcp.tfvars

Build infrastructure
~~~~~~~~~~~~~~~~~~~~

.. code:: shell

   # BILLING_ACCOUNT_ID the billing account to use
   # ORG_ID the organization id
   # PARENT_PROJECT_ID the parent project containing DNS and images
   # PROJECT_ID the id for the project to create
   # PROJECT_NAME its friendly name
   # REGION the region to use

   cd ~/caravan/caravan-infra-gcp
   ./project-setup.sh BILLING_ACCOUNT_ID ORG_ID PARENT_PROJECT_ID PROJECT_ID PROJECT_NAME REGION

The script will provision resources needed for Terraform run:

* a GCP Project linked to a billing account 
* a service account with the needed permissions in the newly created project and the parent one 
* a GCS bucket for state store

This will also create ``gcp.tfvars`` and ``backend.tf`` in the current
directory. You can further edit ``gcp.tvars`` with the needed changes.
For example, you might be interested in setting use_le_staging=true 
to use for Let’s Encrypt staging endpoint and avoid being rate limited
if you are going to run certificate requests too often initially.

The two helper scripts run.sh and destroy.sh can be used to fully
automate the provisioning and destroy of the entire stack, providing a
one-click experience.

To start the provisioning run:

.. code:: shell

   ./run.sh

or

.. code:: shell

   terraform init -reconfigure -upgrade
   terraform apply -var-file gcp.tfvars

Configure the platform
~~~~~~~~~~~~~~~~~~~~~~

.. code:: shell

   cd ~/caravan/caravan-platform
   mv PREFIX-backend.tf.bak backend.tf # replace with your prefix
   terraform init -upgrade -reconfigure
   export VAULT_ADDR=https://vault.PREFIX.EXTERNAL_DOMAIN # replace with your configs
   export VAULT_TOKEN=$(cat ~/caravan/caravan-infra-gcp/.PREFIX-root_token)
   export NOMAD_TOKEN=$(vault read -tls-skip-verify -format=json nomad/creds/token-manager | jq -r .data.secret_id)
   terraform apply -var-file PREFIX-gcp.tfvars # replace with your prefix

Deploy platform applications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: shell

   cd ~/caravan/caravan-application-support
   # repeat as per caravan-platform

Teardown
~~~~~~~~

Destroy resources in all projects via
``terraform destroy -var-file gcp.tfvars``

Alternatively you can use ``destroy.sh`` to automate the entire process.

Delete the resources created via ``project-setup.sh`` script

.. code:: shell

   # PARENT_PROJECT_ID the parent project containing DNS and images
   # PROJECT_ID the id for the project to create

   cd ~/caravan/caravan-infra-gcp
   ./project-cleanup.sh PROJECT_ID PARENT_PROJECT_ID
