## Installation of Azure Kubernetes Service

| Step | Details |
| ----------- | ----------- |
| 1 | Introduction |
| 2 | Terraform Module  |
| 3 | Terraform Workflow - Init  |
| 4 | Terraform Workflow - Plan  |
| 5 | Terraform Workflow - Apply |
| 6 | Walthrough on Azure Portal |
| 7 | Walthrough via az CLI |
| 8 | kubectl connection |
| 9 | Setup Azure Container Registry |
| 10| Sample REST API Application |
| 11| Installation of Ingress Controller |
| 12| Access API over internet (Public IP) |


### 2. Terraform Module
https://developer.hashicorp.com/terraform/tutorials/kubernetes/aks

```
C:\swararoy\installers\terraform\terraform init   

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of hashicorp/azurerm from the dependency lock file
- Reusing previous version of hashicorp/random from the dependency lock file
- Installing hashicorp/azurerm v3.67.0...
- Installed hashicorp/azurerm v3.67.0 (signed by HashiCorp)
- Installing hashicorp/random v3.5.1...
- Installed hashicorp/random v3.5.1 (signed by HashiCorp)

Terraform has made some changes to the provider dependency selections recorded
in the .terraform.lock.hcl file. Review those changes and commit them to your
version control system if they represent changes you intended to make.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

```

```
C:\swararoy\installers\terraform\terraform plan      

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_kubernetes_cluster.default will be created
  + resource "azurerm_kubernetes_cluster" "default" {
      + api_server_authorized_ip_ranges     = (known after apply)
      + dns_prefix                          = (known after apply)
      + fqdn                                = (known after apply)
      + http_application_routing_zone_name  = (known after apply)
      + id                                  = (known after apply)
      + image_cleaner_enabled               = false
      + image_cleaner_interval_hours        = 48
      + kube_admin_config                   = (sensitive value)
      + kube_admin_config_raw               = (sensitive value)
      + kube_config                         = (sensitive value)
      + kube_config_raw                     = (sensitive value)
      + kubernetes_version                  = "1.26.3"
      + location                            = "westus2"
      + name                                = (known after apply)
      + node_resource_group                 = (known after apply)
      + node_resource_group_id              = (known after apply)
      + oidc_issuer_url                     = (known after apply)
      + portal_fqdn                         = (known after apply)
      + private_cluster_enabled             = false
      + private_cluster_public_fqdn_enabled = false
      + private_dns_zone_id                 = (known after apply)
      + private_fqdn                        = (known after apply)
      + public_network_access_enabled       = true
      + resource_group_name                 = (known after apply)
      + role_based_access_control_enabled   = true
      + run_command_enabled                 = true
      + sku_tier                            = "Free"
      + tags                                = {
          + "environment" = "Demo"
        }
      + workload_identity_enabled           = false

      + default_node_pool {
          + kubelet_disk_type    = (known after apply)
          + max_pods             = (known after apply)
          + name                 = "default"
          + node_count           = 2
          + node_labels          = (known after apply)
          + orchestrator_version = (known after apply)
          + os_disk_size_gb      = 30
          + os_disk_type         = "Managed"
          + os_sku               = (known after apply)
          + scale_down_mode      = "Delete"
          + type                 = "VirtualMachineScaleSets"
          + ultra_ssd_enabled    = false
          + vm_size              = "Standard_D2_v2"
          + workload_runtime     = (known after apply)
        }

      + service_principal {
          + client_id     = ""
          + client_secret = (sensitive value)
        }
    }

  # azurerm_resource_group.default will be created
  + resource "azurerm_resource_group" "default" {
      + id       = (known after apply)
      + location = "westus2"
      + name     = (known after apply)
      + tags     = {
          + "environment" = "Demo"
        }
    }

  # random_pet.prefix will be created
  + resource "random_pet" "prefix" {
      + id        = (known after apply)
      + length    = 2
      + separator = "-"
    }

Plan: 3 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + kubernetes_cluster_name = (known after apply)
  + resource_group_name     = (known after apply)

```

```
PS C:\swararoy\2023\code\GITOPS\AKS_INSTALL\learn-terraform-provision-aks-cluster> C:\swararoy\installers\terraform\terraform apply
random_pet.prefix: Refreshing state... [id=talented-silkworm]
azurerm_resource_group.default: Refreshing state... [id=/subscriptions/27860a03-5be0-4d83-992f-78e27af61536/resourceGroups/talented-silkworm-rg]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_kubernetes_cluster.default will be created
  + resource "azurerm_kubernetes_cluster" "default" {
      + api_server_authorized_ip_ranges     = (known after apply)
      + dns_prefix                          = "talented-silkworm-k8s"
      + fqdn                                = (known after apply)
      + http_application_routing_zone_name  = (known after apply)
      + id                                  = (known after apply)
      + image_cleaner_enabled               = false
      + image_cleaner_interval_hours        = 48
      + kube_admin_config                   = (sensitive value)
      + kube_admin_config_raw               = (sensitive value)
      + kube_config                         = (sensitive value)
      + kube_config_raw                     = (sensitive value)
      + kubernetes_version                  = "1.26.3"
      + location                            = "westus2"
      + name                                = "talented-silkworm-aks"
      + node_resource_group                 = (known after apply)
      + node_resource_group_id              = (known after apply)
      + oidc_issuer_url                     = (known after apply)
      + portal_fqdn                         = (known after apply)
      + private_cluster_enabled             = false
      + private_cluster_public_fqdn_enabled = false
      + private_dns_zone_id                 = (known after apply)
      + private_fqdn                        = (known after apply)
      + public_network_access_enabled       = true
      + resource_group_name                 = "talented-silkworm-rg"
      + role_based_access_control_enabled   = true
      + run_command_enabled                 = true
      + sku_tier                            = "Free"
      + tags                                = {
          + "environment" = "Demo"
        }
      + workload_identity_enabled           = false

      + default_node_pool {
          + kubelet_disk_type    = (known after apply)
          + max_pods             = (known after apply)
          + name                 = "default"
          + node_count           = 2
          + node_labels          = (known after apply)
          + orchestrator_version = (known after apply)
          + os_disk_size_gb      = 30
          + os_disk_type         = "Managed"
          + os_sku               = (known after apply)
          + scale_down_mode      = "Delete"
          + type                 = "VirtualMachineScaleSets"
          + ultra_ssd_enabled    = false
          + vm_size              = "Standard_D2_v2"
          + workload_runtime     = (known after apply)
        }

      + service_principal {
          + client_id     = "aaa"
          + client_secret = (sensitive value)
        }
    }

Plan: 1 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

azurerm_kubernetes_cluster.default: Creating...
azurerm_kubernetes_cluster.default: Still creating... [10s elapsed]
azurerm_kubernetes_cluster.default: Still creating... [4m20s elapsed]
azurerm_kubernetes_cluster.default: Still creating... [4m30s elapsed]
azurerm_kubernetes_cluster.default: Creation complete after 4m38s [id=/subscriptions/27860a03-5be0-4d83-992f-78e27af61536/resourceGroups/talented-silkworm-rg/providers/Microsoft.ContainerService/managedClusters/talented-silkworm-aks]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

Outputs:

kubernetes_cluster_name = "talented-silkworm-aks"
resource_group_name = "talented-silkworm-rg"
```

![image](https://github.com/swarajitroy/gitops/assets/20844803/847cfe8b-9e91-4d66-b5f8-0d8f0b23c9aa)

![image](https://github.com/swarajitroy/gitops/assets/20844803/5f756aa2-2fff-4191-b719-6a4fdbc57d98)

