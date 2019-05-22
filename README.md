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
|aws_vpc_cidr|~|CIDR for VPC|
|aws_vpc_cidr_subnet_private_a|~|CIDR for private subnet a|
|aws_vpc_cidr_subnet_private_b|~|CIDR for private subnet b|
|aws_vpc_cidr_subnet_private_c|~|CIDR for private subnet c|
|aws_vpc_cidr_subnet_public_a|~|CIDR for public subnet a|
|aws_vpc_cidr_subnet_public_b|~|CIDR for public subnet b|
|aws_vpc_cidr_subnet_public_c|~|CIDR for public subnet c|
|aws_vpc_region|~|AWS region for VPC|
|aws_vpc_stack_name|~|Name for VPC CF stack|
|aws_vpc_tags|~|Tags for the VPC, you must specify a Name tag|

## Examples

Simply include role in your playbook

```YAML
- name: Install aws_vpc with one subnets
  hosts: somehost

  roles:
    - role: sansible.aws_vpc
      aws_vpc_cidr: 10.0.0.0/21
      aws_vpc_cidr_subnet_private_a: 10.1.0.0/24
      aws_vpc_cidr_subnet_public_a: 10.1.1.0/24
      aws_vpc_region: eu-west-1
      aws_vpc_stack_name: dev-vpc
      aws_vpc_tags:
        Name: dev_vpc
```

```YAML
- name: Install aws_vpc with three subnets
  hosts: somehost

  roles:
    - role: sansible.aws_vpc
      aws_vpc_cidr: 10.0.0.0/21
      aws_vpc_cidr_subnet_private_a: 10.1.0.0/24
      aws_vpc_cidr_subnet_private_b: 10.1.1.0/24
      aws_vpc_cidr_subnet_private_c: 10.1.2.0/24
      aws_vpc_cidr_subnet_public_a: 10.1.3.0/24
      aws_vpc_cidr_subnet_public_b: 10.1.4.0/24
      aws_vpc_cidr_subnet_public_c: 10.1.5.0/24
      aws_vpc_region: eu-west-1
      aws_vpc_stack_name: dev-vpc
      aws_vpc_tags:
        Name: dev_vpc
```