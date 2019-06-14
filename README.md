# aws_vpc

Master: [![Build Status](https://travis-ci.org/sansible/aws_vpc.svg?branch=master)](https://travis-ci.org/sansible/aws_vpc)
Develop: [![Build Status](https://travis-ci.org/sansible/aws_vpc.svg?branch=develop)](https://travis-ci.org/sansible/aws_vpc)

* [Installation and Dependencies](#installation-and-dependencies)
* [Role Variables](#role-variables)
* [Examples](#examples)

This role creates an AWS VPC 1 to 3 private and public subnets complete with route tables and an internet gateway.


## Installation and Dependencies

To install run `ansible-galaxy install sansible.aws_vpc` or add this to your
`roles.yml`.

```YAML
- name: sansible.aws_vpc
  version: v1.0
```

and run `ansible-galaxy install -p ./roles -r roles.yml`

## Role Variables

|Variable|Default|Description|
|---|---|---|
|sansible_aws_vpc_cidr|~|CIDR for VPC|
|sansible_aws_vpc_cidr_subnet_private_a|~|CIDR for private subnet a|
|sansible_aws_vpc_cidr_subnet_private_b|~|Optional CIDR for private subnet b|
|sansible_aws_vpc_cidr_subnet_private_c|~|Optional CIDR for private subnet c|
|sansible_aws_vpc_cidr_subnet_public_a|~|Optional CIDR for public subnet a|
|sansible_aws_vpc_cidr_subnet_public_b|~|Optional CIDR for public subnet b|
|sansible_aws_vpc_cidr_subnet_public_c|~|Optional CIDR for public subnet c|
|sansible_aws_vpc_region|~|AWS region for VPC|
|sansible_aws_vpc_stack_name|~|Name for VPC CF stack|
|sansible_aws_vpc_tags|~|Tags for the VPC, you must specify a Name tag|

## Examples

Simply include role in your playbook

```YAML
- name: Install aws_vpc with one subnets
  hosts: somehost

  roles:
    - role: sansible.aws_vpc
      sansible_aws_vpc_cidr: 10.0.0.0/21
      sansible_aws_vpc_cidr_subnet_private_a: 10.1.0.0/24
      sansible_aws_vpc_cidr_subnet_public_a: 10.1.1.0/24
      sansible_aws_vpc_region: eu-west-1
      sansible_aws_vpc_stack_name: dev-vpc
      sansible_aws_vpc_tags:
        Name: dev_vpc
```

```YAML
- name: Install aws_vpc with no public subnets
  hosts: somehost

  roles:
    - role: sansible.aws_vpc
      sansible_aws_vpc_cidr: 10.0.0.0/21
      sansible_aws_vpc_cidr_subnet_private_a: 10.1.0.0/24
      sansible_aws_vpc_cidr_subnet_private_b: 10.1.1.0/24
      sansible_aws_vpc_cidr_subnet_private_c: 10.1.2.0/24
      sansible_aws_vpc_region: eu-west-1
      sansible_aws_vpc_stack_name: dev-vpc
      sansible_aws_vpc_tags:
        Name: dev_vpc
```

```YAML
- name: Install aws_vpc with a mixed amount of subnets
  hosts: somehost

  roles:
    - role: sansible.aws_vpc
      sansible_aws_vpc_cidr: 10.0.0.0/21
      sansible_aws_vpc_cidr_subnet_private_a: 10.1.0.0/24
      sansible_aws_vpc_cidr_subnet_private_b: 10.1.1.0/24
      sansible_aws_vpc_cidr_subnet_private_c: 10.1.2.0/24
      sansible_aws_vpc_cidr_subnet_public_a: 10.1.1.0/24
      sansible_aws_vpc_region: eu-west-1
      sansible_aws_vpc_stack_name: dev-vpc
      sansible_aws_vpc_tags:
        Name: dev_vpc
```