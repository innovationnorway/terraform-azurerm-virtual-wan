# Azure Virtual WAN Module

![test](https://github.com/innovationnorway/terraform-azurerm-virtual-wan/workflows/test/badge.svg)

This [Terraform](https://www.terraform.io/docs) module manages [Azure Virtual WAN](https://docs.microsoft.com/en-us/azure/virtual-wan/).

```hcl
resource "azurerm_resource_group" "example" {
  name     = "example-rg"
  location = "westeurope"
}

module "wan" {
  source = "innovationnorway/virtual-wan/azurerm"

  name_prefix = "example-vwan"

  resource_group_name = azurerm_resource_group.example.name

  hubs = [
    {
      region = "westeurope"
      prefix = "10.1.0.0/16"
    },
    {
      region = "northeurope"
      prefix = "10.2.0.0/16"
    },
  ]
}
```

## Arguments

* `name` - (Required) The name of the virtual WAN.	

* `resource_group_name` - (Required) The name of the resource group in which to create the resources.	

* `hubs` - (Required) - A list of hubs to create within the virtual WAN. This should be a list of `hubs` objects as described below.

The `hubs` object supports the following:

* `region` - (Required) The Azure region where the virtual hub should be created.

* `prefix` - (Required) The address prefix which should be used for the virtual hub.
