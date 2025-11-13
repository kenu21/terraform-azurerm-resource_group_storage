# Terraform Azure Resource Group and Storage Account Module

This Terraform module creates an **Azure Resource Group** and an **Azure Storage Account**. It is designed to be reusable and configurable for different projects.

## Module Usage

### 1. Add the Module to Your Configuration

In your main Terraform configuration, use the module from GitHub or Terraform Registry:

```hcl
module "resource_group_storage" {
  source = "git::https://github.com/kenu21/terraform-azurerm-resource_group_storage.git?ref=v1.0.0"

  resource_group_name      = "my-resource-group"
  location                 = "East US"
  storage_account_name     = "mystorageacct123"
  account_tier             = "Standard"
  account_replication_type = "LRS"
}
```

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

### 4. How to Apply

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

4. Confirm the outputs and verify the resources in your Azure portal.

---

### 5. Notes

* Ensure your Azure CLI is logged in and Terraform is configured to use the correct subscription.
* The `storage_account_name` must be globally unique across Azure.
* The module follows best practices and allows customization via variables.
