# Tutorials: Terraform Azure AppService Plan

## What you will build

Create a new [AppService Plan][az-appservice-plan] in Azure using open-source [Terraform][terraform]. This will use the [Terraform Azure Provider][terraform-azurerm] for ["app_service_plan"][terraform-app_service_plan].

## What you will need

The following prerequisites are required in order to follow the steps in this tutorial:

- A [Microsoft Azure account][azure-account] with an existing resource group and permission to create an AppService Plan. _\*See the tutorial to [create a new resource group][tutorial-rg]._
- [git]
- [make]
- [docker]

## Build and run

In this section, you will clone the tutorial and execute it:

1. Open a terminal window.

2. If you don't already have one, make a local directory to hold the code and change to that directory by typing `mkdir ./tutorials && cd ./tutorials`.

3. Clone the tutorial into the directory you created by typing:

   ```shell
     git clone https://github.com/ourchitecture/patterns-and-tutorials --depth=1
   ```

4. Change to the directory of this tutorial project by typing `cd ./src/tutorials/terraform/azure/appservice-plan`.

5. Type `make prerequisites` and read the output to verify you have the right tools. Output should look similar to:

   ```shell
   make prerequisites
    Git 2.20 or later is required. You have:
    git version 2.25.1

    Docker 19.03.0 or later is required. You have:
    Docker version 19.03.13, build 4484c46d9d
   ```

6. Test the terraform setup by typing `make test`. You should see output similar to the below.

   ```shell
   make test
     Clearing existing '.terraform' directory (if exists)...
     Initializing terraform without a backend...

     Initializing provider plugins...
     - Finding hashicorp/azurerm versions matching "2.37.0"...
     - Installing hashicorp/azurerm v2.37.0...
     - Installed hashicorp/azurerm v2.37.0 (signed by HashiCorp)

     Terraform has been successfully initialized!

     You may now begin working with Terraform. Try running "terraform plan" to see any changes that are required for your infrastructure. All Terraform commands should now work.

     If you ever set or change modules or backend configuration for Terraform, rerun this command to reinitialize your working directory. If you forget, other commands will detect it and remind you to do so if necessary.
     Checking terraform formatting...
     Validating terraform...
     Success! The configuration is valid.
   ```

7. Review the variable values used to create the plan by opening the file "./tutorial.tfvars". Change the values as needed. The resource group name should already exist and the plan name should not already be used in the group. Choose "Linux" or "Windows" for the "plan_kind". SKU tier examples include Free, Shared, Basic, Premium, and Isolated and SKU size examples include F1 (Free), D1 (Shared), B1 (Basic Small), B2 (Basic Medium), B3 (Basic Large), S1 (Standard Small), P1V2 (Premium V2 Small), P1V3 (Premium V3 Small), P2V3 (Premium V3 Medium), P3V3 (Premium V3 Large), PC2 (Premium Container Small), PC3 (Premium Container Medium), PC4 (Premium Container Large), I1 (Isolated Small), I2 (Isolated Medium), I3 (Isolated Large).

8. Create the plan by typing `make create`. If you want to see what will be created prior to executing this command, type `make plan-create`. If you receive output containing the error "AuthorizationFailed", please contact your Azure administrator to check the permissions for your account.

9. Verify the resource has been created by typing `make list-plans` and checking if the name you assigned to the variable "plan_name" in the "tutorial.tfvars" file exists in the list.

10. To remove the new plan, type `make destroy`. If you want to see what will be destroyed prior to executing this command, type `make plan-destroy`.

[az-appservice-plan]: https://docs.microsoft.com/en-us/azure/app-service/overview-hosting-plans
[terraform]: https://www.terraform.io/intro/index.html
[azure-account]: https://azure.microsoft.com/en-us/free/
[azure-geo]: https://azure.microsoft.com/en-us/global-infrastructure/geographies/
[git]: ../../../../tools/git/README.md
[make]: ../../../../tools/make/README.md
[docker]: ../../../../tools/docker/README.md
[tutorial-rg]: ../resource-group/README.md
[terraform-azurerm]: https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs
[terraform-app_service_plan]: https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/app_service_plan