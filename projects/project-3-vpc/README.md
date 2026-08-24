# Project 3 — Custom AWS VPC & Web Server Deployment

## Project Overview

Built a custom Amazon VPC with separate public and private subnets, configured routing and internet connectivity, and deployed a personal portfolio website on an Amazon EC2 instance running Nginx.

## Objective

The goal of this project was to gain practical experience with AWS networking and understand how VPC components work together to provide secure and controlled network connectivity.

## Architecture

Internet
    |
    v
Internet Gateway
    |
    v
Public Route Table
0.0.0.0/0 -> Internet Gateway
    |
    v
Public Subnet
10.0.1.0/24
    |
    v
EC2 Instance
Amazon Linux 2023
    |
    v
Nginx Web Server
    |
    v
Portfolio Website

Private Subnet
10.0.2.0/24
    |
    v
Private Route Table
(Local VPC route only)

## AWS Services Used

- Amazon VPC
- Amazon EC2
- Amazon VPC Subnets
- Internet Gateway
- Route Tables
- Security Groups
- Amazon EBS

## Technologies

- Amazon Linux 2023
- Nginx
- SSH
- SCP
- HTML/CSS
- Git/GitHub

## Network Configuration

### VPC

CIDR block:

10.0.0.0/16

### Public Subnet

CIDR:

10.0.1.0/24

The public subnet was associated with a route table containing:

0.0.0.0/0 -> Internet Gateway

### Private Subnet

CIDR:

10.0.2.0/24

The private subnet was associated with a separate route table without a direct internet route.

## Implementation

### 1. Created the VPC

Created a custom VPC using the CIDR block:

10.0.0.0/16

### 2. Created the Subnets

Created:

- Public subnet: 10.0.1.0/24
- Private subnet: 10.0.2.0/24

The subnets were placed in different Availability Zones.

### 3. Created an Internet Gateway

Created and attached an Internet Gateway to the custom VPC.

### 4. Configured the Public Route Table

Created a public route table and added:

0.0.0.0/0 -> Internet Gateway

The route table was associated with the public subnet.

### 5. Configured the Private Route Table

Created a separate private route table and associated it with the private subnet.

The private subnet was not given a direct route to the Internet Gateway.

### 6. Launched EC2

Launched a t3.micro EC2 instance using Amazon Linux 2023 inside the public subnet.

A security group was configured to allow SSH access from my IP address.

### 7. Connected Using SSH

Connected to the EC2 instance from Windows Git Bash using an RSA private key.

### 8. Tested Network Connectivity

Used Linux networking commands including:

```bash
ip addr
ip route
