# Getting Started with Terraform
Terraform is the most popular language for defining and provisioning Infrastructure as Code (IaC). This step by step tutorial was designed to get you started quickly with Terraform.

### Learning Objectives
After completing this tutorial, you should be able to:
- Execute the steps to install Terraform
- Describe what happens in the Create, Manage, and Destroy phases of Terraform and be able to give an example

## Prerequisites
- Basic terminal skills
- Basic understanding of Infrastructure as Code - [What is Infrastructure as Code with Terraform?](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/infrastructure-as-code)
- To get the most out of this tutorial, you should be familiar with Terraform - [What is Terraform?](https://developer.hashicorp.com/terraform/intro)

## Install 
To install Terraform, visit [Install Terraform](https://developer.hashicorp.com/terraform/install) and download the compressed binary application executable file deliverable for your platform, machine or environment on which you like to run code and do development.

With Terraform installed, let's dive right into it and start creating some infrastructure.

## Create
In the **Create** phase you configure Terraform to manage your infrastructure.

Most people find it easiest to create a new directory on their local machine and create Terraform configuration code inside it.

```shell
$ mkdir terraform-demo
$ cd terraform-demo
```

Next, create a file for your Terraform configuration code.

```shell
$ touch main.tf
```

Paste the following lines into the file.

```hcl
terraform {
  required_providers {
    docker = {
      source = "kreuzwerker/docker"
    }
  }
}
provider "docker" {
    host = "unix:///var/run/docker.sock"
}
resource "docker_container" "nginx" {
  image = docker_image.nginx.latest
  name  = "training"
  ports {
    internal = 80
    external = 80
  }
}
resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```
## Manage
In the **Manage** phase, you are able to modify and execute Terraform on your infrasturcture. 

Initialize Terraform with the `init` command. The AWS provider will be installed. 

```shell
$ terraform init
```

You should check for any errors. If it ran successfully, provision the resource with the `apply` command.

```shell
$ terraform apply
```

The command will take up to a few minutes to run and will display a message indicating that the resource was created.

## Destroy
In the **Destory** phase, you can destroy the infrastructure you no longer need.

```shell
$ terraform destroy
```

Look for a message are the bottom of the output asking for confirmation. Type `yes` and hit ENTER. Terraform will destroy the resources it had created earlier.

## Next Steps
In this tutorial you learned how to install Terraform on the platform of your choice. You then used sample code in the **Create** phase to create a Terraform configuration. In the **Manage** phase you initialized and applied your Terraform configuration. Finally, in the **Destroy** phase to destroyed all the resources you created. 

Looking for a more exhaustive tutorial? [Terraform](https://developer.hashicorp.com/terraform)
Interested in Certification? [Infrastructure Automation Certifications](https://developer.hashicorp.com/certifications/infrastructure-automation)
