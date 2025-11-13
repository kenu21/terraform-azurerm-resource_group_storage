# Terraform Azure Resource Group and Storage Account Module

This Terraform module creates an **Azure Resource Group** and an **Azure Storage Account**. It is designed to be reusable and configurable for different projects, allowing you to quickly provision resources in Azure.

## Module Usage

### 1. Include the Module in Your Configuration

You can use this module either from GitHub or from the Terraform Registry:

```hcl
module "resource_group_storage" {
  source = "git::https://github.com/kenu21/terraform-azurerm-resource_group_storage.git?ref=v1.0.0"

  resource_group_name      = "my-resource-group"
  location                 = "East US"
  storage_account_name     = "mystorageacct123"
  account_tier             = "Standard"
  account_replication_type = "LRS"
}
````

---

### 2. Module Variables

| Variable Name              | Description                                                  | Type   | Default    |
| -------------------------- | ------------------------------------------------------------ | ------ | ---------- |
| `resource_group_name`      | Name of the resource group                                   | string | n/a        |
| `location`                 | Azure region to deploy resources                             | string | `East US`  |
| `storage_account_name`     | Name of the storage account                                  | string | n/a        |
| `account_tier`             | Tier of the storage account (`Standard` or `Premium`)        | string | `Standard` |
| `account_replication_type` | Replication type of the storage account (`LRS`, `GRS`, etc.) | string | `LRS`      |

---

### 3. Module Outputs

| Output Name                            | Description                                 |
| -------------------------------------- | ------------------------------------------- |
| `resource_group_name`                  | Name of the created resource group          |
| `storage_account_name`                 | Name of the created storage account         |
| `storage_account_primary_web_endpoint` | Primary web endpoint of the storage account |

---

### 4. Example

```hcl
provider "azurerm" {
  features {}
}

module "resource_group_storage" {
  source = "git::https://github.com/kenu21/terraform-azurerm-resource_group_storage.git?ref=v1.0.0"

  resource_group_name      = "example-rg"
  location                 = "East US"
  storage_account_name     = "examplestorage123"
  account_tier             = "Standard"
  account_replication_type = "LRS"
}

output "resource_group" {
  value = module.resource_group_storage.resource_group_name
}

output "storage_account" {
  value = module.resource_group_storage.storage_account_name
}

output "storage_endpoint" {
  value = module.resource_group_storage.storage_account_primary_web_endpoint
}
```

---

### 5. How to Apply

1. Initialize Terraform:

```bash
terraform init
```

2. Plan your changes:

```bash
terraform plan
```

3. Apply the configuration:

```bash
terraform apply
```

4. Verify the outputs and check the resources in your Azure portal.

---

### 6. Notes

* Ensure your Azure CLI is logged in and Terraform is configured to use the correct subscription.
* `storage_account_name` must be globally unique across Azure.
* The module is designed for reusability and supports customization via input variables.
