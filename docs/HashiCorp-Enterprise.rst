HashiCorp Enterprise
====================

Caravan supports deploying the enterprise versions of HashiCorp Vault,
Consul and Nomad.

Building Enterprise images
--------------------------

`caravan-baking <https://github.com/bitrockteam/caravan-baking>`__
supports building gold images with either OpenSource or Enterprise
binaries for HashiCorp stack.

By default, the Terraform wrapper used to trigger Packer builds creates
both image types:

.. code:: hcl

   variable "builds" {
     type        = list(string)
     default     = ["caravan.*.enterprise", "caravan.*.opensource"]
     description = "Which packer build artifacts to produce"
   }

   variable "build_image_name" {
     type = string
   }

   //...

The resulting image name follows the following pattern: -
``${var.build_image_name}-os-{{timestamp}}`` for OpenSource version -
``${var.build_image_name}-ent-{{timestamp}}`` for Enterprise version

Deploying Enterprise infrastructure
-----------------------------------

Once you have built the image with Enterprise binaries, the next steps
are:

1. Configure the image filter variable in the infrastructure layer to
   use the Enterprise image instead of the OpenSource one. For example,
   in Azure you have to change ``var.image_name_regex`` value:

.. code:: hcl

   image_name_regex = "caravan-centos-image-ent-*"

2. Provide license files via the dedicated input variables:

.. code:: hcl

   consul_license_file = "path/to/consul.hclic"
   vault_license_file  = "path/to/vault.hclic"
   nomad_license_file  = "path/to/nomad.hclic"
