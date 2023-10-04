## Installation of Azure Kubernetes Service

| Step | Details |
| ----------- | ----------- |
| 1 | Introduction |
| 2 | Terraform Module  |
| 3 | Terraform Workflow - Init, Plan, Apply, Destroy |
| 4 | Walthrough on Azure Portal |
| 5 | kubectl connection |
| 6 | Setup Azure Container Registry |
| 7 | Sample REST API Application |
| 8 | Installation of Ingress Controller |
| 9 | Access API over internet (Public IP) |


### 2. Terraform Module
https://developer.hashicorp.com/terraform/tutorials/kubernetes/aks

### 3. Terraform Workflow - Init, Plan, Apply, Destroy
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
azurerm_resource_group.default: Refreshing state... [id=/subscriptions/278661536/resourceGroups/talented-silkworm-rg]

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
azurerm_kubernetes_cluster.default: Creation complete after 4m38s [id=/subscriptions/27860a6/resourceGroups/talented-silkworm-rg/providers/Microsoft.ContainerService/managedClusters/talented-silkworm-aks]

Apply complete! Resources: 1 added, 0 changed, 0 destroyed.

Outputs:

kubernetes_cluster_name = "talented-silkworm-aks"
resource_group_name = "talented-silkworm-rg"
```

```
PS C:\swararoy\2023\code\GITOPS\AKS_INSTALL\learn-terraform-provision-aks-cluster> C:\swararoy\installers\terraform\terraform destroy                         
random_pet.prefix: Refreshing state... [id=talented-silkworm]
azurerm_resource_group.default: Refreshing state... [id=/subscriptions/27868e27af61536/resourceGroups/talented-silkworm-rg]
azurerm_kubernetes_cluster.default: Refreshing state... [id=/subscriptions/2787af61536/resourceGroups/talented-silkworm-rg/providers/Microsoft.ContainerService/managedClusters/talented-silkworm-aks]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # azurerm_kubernetes_cluster.default will be destroyed
  - resource "azurerm_kubernetes_cluster" "default" {
      - api_server_authorized_ip_ranges     = [] -> null
      - custom_ca_trust_certificates_base64 = [] -> null
      - dns_prefix                          = "talented-silkworm-k8s" -> null
      - enable_pod_security_policy          = false -> null
      - fqdn                                = "talented-silkworm-k8s-b08awjsh.hcp.westus2.azmk8s.io" -> null
      - id                                  = "/subscriptions/1536/resourceGroups/talented-silkworm-rg/providers/Microsoft.ContainerService/managedClusters/talented-silkworm-aks" -> null
      - image_cleaner_enabled               = false -> null
      - image_cleaner_interval_hours        = 48 -> null
      - kube_admin_config                   = (sensitive value) -> null
      - kube_config                         = (sensitive value) -> null
      - kube_config_raw                     = (sensitive value) -> null
      - kubernetes_version                  = "1.26.3" -> null
      - local_account_disabled              = false -> null
      - location                            = "westus2" -> null
      - name                                = "talented-silkworm-aks" -> null
      - node_resource_group                 = "MC_talented-silkworm-rg_talented-silkworm-aks_westus2" -> null
      - node_resource_group_id              = "/subscriptions/abc/resourceGroups/MC_talented-silkworm-rg_talented-silkworm-aks_westus2" -> null
      - oidc_issuer_enabled                 = false -> null
      - portal_fqdn                         = "talented-silkworm-k8s-b08awjsh.portal.hcp.westus2.azmk8s.io" -> null
      - private_cluster_enabled             = false -> null
      - private_cluster_public_fqdn_enabled = false -> null
      - public_network_access_enabled       = true -> null
      - resource_group_name                 = "talented-silkworm-rg" -> null
      - role_based_access_control_enabled   = true -> null
      - run_command_enabled                 = true -> null
      - sku_tier                            = "Free" -> null
      - tags                                = {
          - "environment" = "Demo"
        } -> null
      - workload_identity_enabled           = false -> null

      - default_node_pool {
          - custom_ca_trust_enabled      = false -> null
          - enable_auto_scaling          = false -> null
          - enable_host_encryption       = false -> null
          - enable_node_public_ip        = false -> null
          - fips_enabled                 = false -> null
          - kubelet_disk_type            = "OS" -> null
          - max_count                    = 0 -> null
          - max_pods                     = 110 -> null
          - min_count                    = 0 -> null
          - name                         = "default" -> null
          - node_count                   = 2 -> null
          - node_labels                  = {} -> null
          - node_taints                  = [] -> null
          - only_critical_addons_enabled = false -> null
          - orchestrator_version         = "1.26.3" -> null
          - os_disk_size_gb              = 30 -> null
          - os_disk_type                 = "Managed" -> null
          - os_sku                       = "Ubuntu" -> null
          - scale_down_mode              = "Delete" -> null
          - tags                         = {} -> null
          - type                         = "VirtualMachineScaleSets" -> null
          - ultra_ssd_enabled            = false -> null
          - vm_size                      = "Standard_D2_v2" -> null
          - zones                        = [] -> null
        }

      - network_profile {
          - dns_service_ip    = "10.0.0.10" -> null
          - ip_versions       = [
              - "IPv4",
            ] -> null
          - load_balancer_sku = "standard" -> null
          - network_plugin    = "kubenet" -> null
          - outbound_type     = "loadBalancer" -> null
          - pod_cidr          = "10.244.0.0/16" -> null
          - pod_cidrs         = [
              - "10.244.0.0/16",
            ] -> null
          - service_cidr      = "10.0.0.0/16" -> null
          - service_cidrs     = [
              - "10.0.0.0/16",
            ] -> null

          - load_balancer_profile {
              - effective_outbound_ips      = [
                  - "/subscriptions/278601536/resourceGroups/MC_talented-silkworm-rg_talented-silkworm-aks_westus2/providers/Microsoft.Network/publicIPAddresses/44c09cbb-b515-462a-b96a-2e56f39ec4c2",
                ] -> null
              - idle_timeout_in_minutes     = 0 -> null
              - managed_outbound_ip_count   = 1 -> null
              - managed_outbound_ipv6_count = 0 -> null
              - outbound_ip_address_ids     = [] -> null
              - outbound_ip_prefix_ids      = [] -> null
              - outbound_ports_allocated    = 0 -> null
            }
        }

      - service_principal {
          - client_id     = abc" -> null
          - client_secret = (sensitive value) -> null
        }
    }

  # azurerm_resource_group.default will be destroyed
  - resource "azurerm_resource_group" "default" {
      - id       = "/subscriptions/27860a0af61536/resourceGroups/talented-silkworm-rg" -> null
      - location = "westus2" -> null
      - name     = "talented-silkworm-rg" -> null
      - tags     = {
          - "environment" = "Demo"
        } -> null
    }

  # random_pet.prefix will be destroyed
  - resource "random_pet" "prefix" {
      - id        = "talented-silkworm" -> null
      - length    = 2 -> null
      - separator = "-" -> null
    }

Plan: 0 to add, 0 to change, 3 to destroy.

Changes to Outputs:
  - kubernetes_cluster_name = "talented-silkworm-aks" -> null
  - resource_group_name     = "talented-silkworm-rg" -> null

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

azurerm_kubernetes_cluster.default: Destroying... [id=/subscriptions/27860a36/resourceGroups/talented-silkworm-rg/providers/Microsoft.ContainerService/managedClusters/talented-silkworm-aks]
azurerm_kubernetes_cluster.default: Still destroying... [id=/subscriptions/278683-992f-.../managedClusters/talented-silkworm-aks, 10s elapsed]
azurerm_kubernetes_cluster.default: Still destroying... [id=/subscriptions/27865be0-4d83-992f-.../managedClusters/talented-silkworm-aks, 3m20s elapsed]  
azurerm_kubernetes_cluster.default: Destruction complete after 3m21s
azurerm_resource_group.default: Destroying... [id=/subscriptions/27860a36/resourceGroups/talented-silkworm-rg]
azurerm_resource_group.default: Still destroying... [id=/subscriptions/27860a03-5f-...36/resourceGroups/talented-silkworm-rg, 1m50s elapsed]    azurerm_resource_group.default: Destruction complete after 1m57s
random_pet.prefix: Destroying... [id=talented-silkworm]
random_pet.prefix: Destruction complete after 0s

Destroy complete! Resources: 3 destroyed.
```

### 4. Walthrough on Azure Portal

![image](https://github.com/swarajitroy/gitops/assets/20844803/847cfe8b-9e91-4d66-b5f8-0d8f0b23c9aa)

![image](https://github.com/swarajitroy/gitops/assets/20844803/5f756aa2-2fff-4191-b719-6a4fdbc57d98)

### 5. kubectl configuration

```
az aks get-credentials --resource-group talented-silkworm-rg --name talented-silkworm-aks --file kubeconfig-ss
Merged "talented-silkworm-aks" as current context in kubeconfig-ss
```

Copy the file into $HOME/.kube/config

```
kubectl get nodes
NAME                              STATUS   ROLES   AGE   VERSION
aks-default-37703709-vmss000000   Ready    agent   29m   v1.26.3
aks-default-37703709-vmss000001   Ready    agent   29m   v1.26.3
```

### 6. Install Azure Container Registry 

https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/container_registry


### 8. Installation of Ingress Controller

First - ensure you have helm installed.

```
C:\swararoy\installers\helm\helm version
version.BuildInfo{Version:"v3.13.0", GitCommit:"825e86f6a7a38cef1112bfa606e4127a706749b1", GitTreeState:"clean", GoVersion:"go1.20.8"}
```

Next get a public IP created

```
az network public-ip create --resource-group AKSPublicIP_RG  --name myAKSPublicIPForIngress --sku Standard  --allocation-method static
```
