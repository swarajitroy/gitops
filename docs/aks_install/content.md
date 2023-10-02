## Installation of Azure Kubernetes Service

| Step | Details |
| ----------- | ----------- |
| 1 | App Registration in Azure Active Directory |
| 2 | Suitable Terraform Module  |
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
