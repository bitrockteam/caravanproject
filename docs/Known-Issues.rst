In this page we list the known issues and possible workarounds

Application Support
-------------------

Failed to delete ‘global’ config entry
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When destroying the Application Support layer

::

   Error: Failed to delete 'global' config entry: &errors.errorString{s:"Unexpected response code: 500 (rpc error making call: service \"default/jaeger-query\" has protocol \"tcp\", which does not match defined listener protocol \"http\")"}

Solution
^^^^^^^^

https://github.com/bitrockteam/caravan-application-support/issues/33

Azure
-----

Error ensuring Resource Providers are registered
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   Error: Error ensuring Resource Providers are registered.

   Terraform automatically attempts to register the Resource Providers it supports to
   ensure it's able to provision resources.

   If you don't have permission to register Resource Providers you may wish to use the
   "skip_provider_registration" flag in the Provider block to disable this functionality.

   Please note that if you opt out of Resource Provider Registration and Terraform tries
   to provision a resource from a Resource Provider which is unregistered, then the errors
   may appear misleading - for example:

   > API version 2019-XX-XX was not found for Microsoft.Foo

   Could indicate either that the Resource Provider "Microsoft.Foo" requires registration,
   but this could also indicate that this Azure Region doesn't support this API version.

   More information on the "skip_provider_registration" flag can be found here:
   https://www.terraform.io/docs/providers/azurerm/index.html#skip_provider_registration

   Original Error: Cannnot register providers: Microsoft.AVS. Errors were: Cannot register provider Microsoft.AVS with Azure Resource Manager: resources.ProvidersClient#Register: Failure responding to request: StatusCode=403 -- Original Error: autorest/azure: Service returned an error. Status=403 Code="AuthorizationFailed" Message="The client 'xxxx' with object id 'yyyy' does not have authorization to perform action 'Microsoft.AVS/register/action' over scope '/subscriptions/zzzz' or the scope is invalid. If access was recently granted, please refresh your credentials.".

.. _solution-1:

Solution
^^^^^^^^

Take note of the provider failing to register, in our case
“Microsoft.AVS”. With a privileged account configured locally, manually
register the provider via CLI:

::

   az provider register -n Microsoft.AVS --wait

Error destroying infrastructure layer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When running ``terraform destroy`` in ``caravan-infra-azure`` it might
be possible that the operation fails due to parallelism at the provider
level. For example:

::

   Error: Error waiting for removal of Application Gateway Backend Address Pool Association for NIC "ripa8-monitoring" (Resource Group "ripa8-rg"): Code="OperationNotAllowed" Message="Operation 'startTenantUpdate' is not allowed on VM 'ripa8-monitoring' since the VM is marked for deletion. You can only retry the Delete operation (or wait for an ongoing one to complete)." Details=[]

   Error: removing Network Security Group Association from Subnet "ripa8-subnet" (Virtual Network "ripa8-vnet" / Resource Group "ripa8-rg"): network.SubnetsClient#CreateOrUpdate: Failure sending request: StatusCode=0 -- Original Error: Code="ReferencedResourceNotProvisioned" Message="Cannot proceed with operation because resource /subscriptions/xxxx/resourceGroups/ripa8-rg/providers/Microsoft.Network/networkInterfaces/ripa8-monitoring/ipConfigurations/internal used by resource /subscriptions/xxx/resourceGroups/ripa8-rg/providers/Microsoft.Network/virtualNetworks/ripa8-vnet/subnets/ripa8-subnet is not in Succeeded state. Resource is in Failed state and the last operation that updated/is updating the resource is PutNicOperation." Details=[]

.. _solution-2:

Solution
^^^^^^^^

You might need to rerun ``terraform destroy`` a couple times

Enterprise
----------

Cannot write to readonly storage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

   Error: error reading from Vault: Error making API request.

   URL: GET https://vault.ripa8.caravan-azure.bitrock.it/v1/sys/internal/ui/mounts/secret/consul/bootstrap_token
   Code: 400. Errors:

   * error performing token check: failed to persist lease entry: cannot write to readonly storage

Solution: this is a random error, retrying the failing command should
result in a success
