Getting started on AWS
######################

Prerequisites
~~~~~~~~~~~~~

Clone repos
^^^^^^^^^^^

.. code:: shell

   mkdir ~/caravan
   cd ~/caravan
   git clone git@github.com:bitrockteam/caravan-baking.git
   git clone git@github.com:bitrockteam/caravan-infra-aws.git
   git clone git@github.com:bitrockteam/caravan-platform.git
   git clone git@github.com:bitrockteam/caravan-application-support.git

Install and configure AWS CLI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Please refer to `AWS User
Guide <https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html>`__
for installing and configuring AWS CLI.

Build VM images
~~~~~~~~~~~~~~~

.. code:: shell

   cd ~/caravan/caravan-baking/terraform

   cat <<EOF > aws.tfvars
   build_on_aws      = true
   build_image_name  = "caravan-centos-image"
   aws_access_key    = "YOUR-ACCESS-KEY"
   aws_secret_key    = "YOUR-SECRET-KEY"
   aws_region        = "eu-central-1"
   aws_instance_type = "t3.small"
   EOF

   terraform init
   terraform apply -var-file aws.tfvars

Build infrastructure
~~~~~~~~~~~~~~~~~~~~

.. code:: shell

   # NAME the prefix to be used for resources
   # REGION where to create resources
   # PROFILE the profile name in ~/.aws/credentials to use

   cd ~/caravan/caravan-infra-aws
   ./project-setup.sh NAME REGION PROFILE

The script will provision resources needed for Terraform run: - S3
Bucket for state store - DynamoDB Table for state locking

This will also create ``aws.tfvars`` and ``backend.tf`` in the current
directory. You can further edit ``aws.tvars`` with the needed changes.
For example, you might be interested in setting ``use_le_staging=true``
for Let’s Encrypt staging endpoint.

You need to have an already existing route53 zone to use and configure
it with ``external_domain`` var in ``aws.tvars``.

The two helper scripts ``run.sh`` and ``destroy.sh`` can be used to
fully automate the provisioning and destroy of the entire stack,
providing a one-click experience.

To start the provisioning run:

.. code:: shell

   ./run.sh

or

.. code:: shell

   terraform init -reconfigure -upgrade
   terraform apply -var-file aws.tfvars

Configure the platform
~~~~~~~~~~~~~~~~~~~~~~

.. code:: shell

   cd ~/caravan/caravan-platform
   export PREFIX=your-prefix # replace with your prefix
   export EXTERNAL_DOMAIN=my-real-domain.io # replace with your external_domain
   mv $PREFIX-aws-backend.tf.bak backend.tf 
   terraform init -upgrade -reconfigure
   export VAULT_ADDR=https://vault.$PREFIX.$EXTERNAL_DOMAIN
   export VAULT_TOKEN="$(cat "../caravan-infra-aws/.$PREFIX-root_token")"
   export NOMAD_TOKEN=$(vault read -tls-skip-verify -format=json nomad/creds/token-manager | jq -r .data.secret_id)
   terraform apply -var-file $PREFIX-aws.tfvars

Deploy platform applications
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: shell

   cd ~/caravan/caravan-application-support
   # repeat as per caravan-platform

Teardown
~~~~~~~~

Destroy resources in all projects via
``terraform destroy -var-file aws.tfvars``.

Alternatively you can use ``destroy.sh`` to automate the entire process.

Delete the resources created via ``project-setup.sh`` script

.. code:: shell

   # NAME the prefix to be used for resources
   # REGION where to create resources
   # PROFILE the profile name in ~/.aws/credentials to use

   cd ~/caravan/caravan-infra-aws
   ./project-cleanup.sh NAME REGION PROFILE
