Welcome to Caravan!
###################

What is Caravan?
----------------

Caravan is your platform builder based on the HashiCorp stack. Terraform
and Packer are used to build and deploy a cloud native and ready to use platform
composed from Vault, Consul and Nomad.

The idea behind Caravan is to provide a one-click experience for
deploying an entire infrastructure and configuration needed for running
the entire HashiCorp stack in your preferred cloud environment. Infrastructure and
Configuration as Code are in the core of Caravan. Caravan supports both
OpenSource and Enterprise versions of HashiCorp products.

The Caravan's code is modular and layered to achieve the maximum flexibility and yet 
cover the most common use cases. Multiple cloud providers and optional components 
can be mixed to achieve specific goals.

Currently supported platforms
-----------------------------

* Amazon Web Services (AWS)
* Google Cloud Platform (GCP)
* Microsoft Azure

.. toctree::
    :maxdepth: 2
    :glob:
    :hidden:

    getting-started-on-aws.rst
    getting-started-on-gcp.rst
    getting-started-on-azure.rst
    hashicorp-enterprise.rst
    deploying-applications.rst
    known-issues.rst
    changelog.rst
