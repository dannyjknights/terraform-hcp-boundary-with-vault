# HashiCorp Boundary

![HashiCorp Boundary Logo](https://www.hashicorp.com/_next/static/media/colorwhite.997fcaf9.svg)

## Overview

HashiCorp Boundary is a secure and efficient way to access distributed infrastructure. It provides secure access to SSH, RDP, and HTTP(S) resources, without the need for VPNs or exposing the infrastructure to the public internet.

This README file explains how to set up a multi-hop deployment using Boundary.

## Multi-hop Deployment using HCP Boundary

HCP Boundary allows for secure access to resources across multiple networks and environments. A multi-hop deployment can be set up to allow users to access resources in a private network, without exposing that network to the Internet. The multi-hop deployment in this repo has been setup as follows:

1. Configure HCP Boundary.
2. Deploy a Boundary Ingress Worker in a public network.
3. Deploy a Boundary Egress Worker in a private network.
3. Establish a connection between the Boundary Controller and the Boundary Workers.
4. Configure Boundary to allow access to resources in the private network.

Your HCP Boundary Cluster needs to be created prior to executing the Terraform code. 

With this setup, users can securely access resources in the private network without needing to connect directly to the network, or expose resources publicly to the Internet

## tfvars Variables

The following tfvars variables have been defined in a terraform.tfvars file. Please note that the `variables.tf` file contains values for `vault_addr`, `vault_token` and `boundary_vault_token`. This is as a result of the ongoing integration with Vault for brokered and injected credentials.

If you do not want to include this and just stick to self-generated SSH credentials, please comment out the code in the `vault-credentials-store.tf` and `vault-policy.tf` files.

- `boundary_addr`: The HCP Boundary address, e.g. "https://xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.boundary.hashicorp.
cloud"
- `auth_method_id`: "ampw_xxxxxxxxxx"                 
                 
- `password_auth_method_login_name`: = ""
- `password_auth_method_password`:   = ""
- `private_vpc_cidr`:                = ""
- `private_subnet_cidr`:             = ""
- `aws_vpc_cidr`:                    = ""
- `aws_subnet_cidr`:                 = ""
- `aws_access`:                      = ""
- `aws_secret`:                      = ""
