Welcome to Caravan!
###################

What is Caravan?
----------------

Caravan is your platform builder based on the HashiCorp stack. Terraform
and Packer are used to build and deploy a cloud native and ready to use platform
composed of `Vault <https://www.hashicorp.com/products/vault>`_, `Consul <https://www.hashicorp.com/products/consul>`_ and `Nomad <https://www.hashicorp.com/products/nomad>`_.

The idea behind `Caravan <https://caravanproject.io/>`_ is to provide a one-click experience to
deploy an entire infrastructure and its configuration needed to run
the full HashiCorp stack in your preferred cloud environment. 

Infrastructure and Configuration as Code are at the core of Caravan. 

Caravan's code base is modular and layered to achieve the maximum flexibility and yet 
cover the most common use cases. Multiple cloud providers and optional components 
can be mixed to achieve specific goals.

Caravan supports both OpenSource and Enterprise versions of HashiCorp products.

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
