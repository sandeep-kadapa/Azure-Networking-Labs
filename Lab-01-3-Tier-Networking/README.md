# Azure Networking Lab 1 — 3-Tier Architecture with Load Balancer

## Overview

This lab demonstrates a practical 3-tier application architecture in Microsoft Azure using Azure networking and security services.

The objective was to build Web, Application, and Database tiers, control communication between the tiers using Network Security Groups (NSGs) and Application Security Groups (ASGs), provide private VM management using Azure Bastion, and expose the Web tier through an Azure Load Balancer.

The lab also included connectivity testing, NSG troubleshooting, and Load Balancer health-probe/failover testing.

## Architecture

The lab implements a 3-tier application architecture in Azure:

- Web Tier — handles HTTP traffic
- Application Tier — handles application-level communication
- Database Tier — provides database connectivity
- Azure Bastion — provides secure management access to private VMs
- Azure Load Balancer — distributes incoming HTTP traffic across Web VMs

### Architecture Diagram

```text
                         Internet
                            |
                            v
                  Azure Load Balancer
                       TCP :80
                            |
                   +--------+--------+
                   |                 |
                   v                 v
              Web VM 01          Web VM 02
              ASG-Web             ASG-Web
                   |                 |
                   +--------+--------+
                            |
                         TCP :443
                            |
                   +--------+--------+
                   |                 |
                   v                 v
              App VM 01          App VM 02
              ASG-App             ASG-App
                   |
                TCP :1433
                   |
                   v
                DB VM 01
                ASG-DB


### VNet Topology

![Azure VNet Topology](./screenshots/VNet-topology.png)

The VNet contains separate subnets for the Web, Application, Database, and Azure Bastion components. This provides logical network segmentation between application tiers.

### VNet and Subnets

![VNet and Subnets](./screenshots/VNet-Subnets.png)


Management Access:

Administrator
     |
 Internet
     |
 Azure Bastion
     |
 Azure VNet
     |
 Private VMs

Network Segmentation:

VNet: 10.10.0.0/16
|
+-- WebSubnet
|   10.10.1.0/24
|   |
|   +-- web-vm-01
|   +-- web-vm-02
|
+-- AppSubnet
|   10.10.2.0/24
|   |
|   +-- app-vm-01
|   +-- app-vm-02
|
+-- DBSubnet
|   10.10.3.0/24
|   |
|   +-- db-vm-01
|
+-- AzureBastionSubnet
    10.10.4.0/26

Traffic Flow:

Internet
   |
   | TCP 80
   v
Load Balancer
   |
   v
Web Tier
   |
   | TCP 443
   v
Application Tier
   |
   | TCP 1433
   v
Database Tier

Security Flow:

Internet → Web :80       ALLOWED
Web → App :443           ALLOWED
App → DB :1433           ALLOWED
Web → DB :1433           DENIED

