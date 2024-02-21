# Terraform IaC Full AWS VPC WebApp Infrastructure

In this project a full AWS VPC environment architecture is deployed dynamically using Terraform.
The architecture includes a new VPC running a WebApp container in a private subnet and an Application Load Balancer routing public traffic to it.
In addition this module will also deploy a *Bastion Host* on another EC2 instance for SSH connections to the private App host. 
The Terraform module deploys all the required AWS services and can be dynamically configured for your own needs.

## Features

- The Terraform modules can be dynamically configured for your needs by stating
  the desired web app Docker image, App name, open ports, AWS region and more.
- Builds and runs the Web App Docker image on an instance in a private subnet using a NAT Gateway.
- Pulls a Web App Docker image from remote registry via *User Data* script.
- Deploys an Application Load Balancer in a public subnet that routes traffic to the App backend.
- Configures all required security groups and routing tables.
- Deploys a Bastion Host for SSH connections to the private EC2.
- Bastion Host SSH key is saved locally and the private EC2 SSH key located in Bastion root directory.


## How to run the deployment:

1. **Clone this repo locally.**

2. **Create AWS account authentication Access Key:**
  - Navigate to *Security credentials* in your AWS account
    and create an Access Key to be used in AWS cli.

3. **Enter your preferences in Terraform .tfvars file:**

    - awscli_cred_dict - *["AWScli/credentials/file/path"]*
    - aws_region - *"your-aws-account-region"*
    - app_docker_image - *"registry/image-name"*
    - image_tag - *"Docker-image-version-tag"*
    - app_name - *"App-name-tag"*
    - container_port - *"port-number-exposed-by-image"*


4. **Install AWS-cli and authenticate your AWS account:**
  - Follow installation guide:
    *https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html*

  - Run configuration:

    ``` bash
    aws configure
      AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
      AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
      Default region name [None]: us-west-2
      Default output format [None]: json
    ```

5. **Install Terraform:**
  - Follow installation guide:
    *https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli*

5. **Initialize main Terraform module:**

  ``` bash
  terraform init
  ```

6. **Run Terraform plan to validate deployment:**

  ``` bash
  terraform plan
  ```

7. **Run Terraform apply to initiate deployment:**

  ``` bash
  terraform apply
  ```

**Your new VPC with two instances will now be available in your AWS account and region as specified.**

**The Web App is available by navigating to your new Load Balancer's public DNS root path.**
