# terraform-aws-sg
Terraform AWS Security Group Module



-->

Terraform module to provision AWS [`Security-Group`]



## Introduction

The module will create:

* Security Group
* Security Group Rules


## Usage


```hcl

include {
  path = find_in_parent_folders()
}


inputs = {
  name   = "rds-sg-test"
  vpc_id = "vpc-0909008009"
  rules = [
    {
      type        = "ingress"
      from_port   = 22
      to_port     = 22
      protocol    = "tcp"
      cidr_blocks = ["129.98.0.0/16"]
      self        = null
      description = "Allow SSH from anywhere"
    },
    {
      type        = "ingress"
      from_port   = 3306
      to_port     = 3306
      protocol    = "tcp"
      cidr_blocks = ["129.98.0.0/16""]
      self        = true
      description = "Allow RDS from inside the security group"
    },
    {
      type        = "ingress"
      from_port   = 3389
      to_port     = 3389
      protocol    = "tcp"
      cidr_blocks = ["129.98.0.0/16""]
      self        = true
      description = "Allow RDP from inside the security group"
    },
    {
      type        = "egress"
      from_port   = 0
      to_port     = 65535
      protocol    = "all"
      cidr_blocks = ["0.0.0.0/0"]
      self        = null
      description = "Allow egress to anywhere"
    }
  ]
  tags = {
    "ucop:application" = "chs"
    "ucop:createdBy"   = "Terraform"
    "ucop:enviroment"  = "Prod"
    "ucop:group"       = "CHS"
    "ucop:source"      = join("/", ["https://github.com/ucopacme/ucop-terraform-config/tree/master/terraform/its-chs-dev/us-west-2", path_relative_to_include()])
    "Name"             = "rds-sg-test"
  }
}

terraform {

  source = "git::https://git@github.com/ucopacme/terraform-aws-sg.git"

}
