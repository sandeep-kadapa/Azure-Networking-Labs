# Azure Networking Labs

Hands-on Azure networking projects created as part of my **AZ-104: Microsoft Azure Administrator** preparation.

The goal of this repository is to move beyond theoretical knowledge and build, configure, troubleshoot, and validate Azure networking components through practical labs.

---

## 🎯 Objective

This repository focuses on developing practical experience with Azure networking, including:

- Azure Virtual Networks and subnetting
- Network Security Groups (NSGs)
- Application Security Groups (ASGs)
- Azure Load Balancer
- Application Gateway
- Azure Front Door
- Azure DNS and Private DNS
- Azure Firewall
- Route Tables and User Defined Routes (UDR)
- VNet Peering
- VPN Gateway
- ExpressRoute
- NAT Gateway
- Network connectivity and troubleshooting

Each lab is designed around a realistic scenario and includes configuration, testing, troubleshooting, screenshots, and lessons learned.

---

# 🧪 Labs

## Lab 01 — 3-Tier Architecture with Load Balancer

### Architecture

A practical 3-tier application architecture was implemented in Azure:

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
```

## Lab 02 — Application Gateway with Path-Based Routing

### Architecture

The lab uses Azure Application Gateway as the public Layer 7 entry point.

Backend VMs remain private and are accessed through Application Gateway for application traffic, Azure Bastion for administration, and NAT Gateway for outbound Internet connectivity.

### Architecture Diagram

```text
                              Internet
                                  |
                                  | HTTP :80
                                  v
                    +---------------------------+
                    |   Azure Application       |
                    |        Gateway            |
                    |      Standard V2          |
                    |       Public IP            |
                    +-------------+-------------+
                                  |
                     HTTP Listener / Path Routing
                                  |
                    +-------------+-------------+
                    |                           |
                 /web/*                      /app/*
                    |                           |
                    v                           v
              +-----------+               +-----------+
              |  bp-web   |               |  bp-app   |
              +-----+-----+               +-----+-----+
                    |                           |
                    v                           v
              web-vm-01                   app-vm-01
              10.20.1.4                   10.20.2.4
                    |                           |
                    +-------------+-------------+
                                  |
                           NAT Gateway
                                  |
                                  v
                              Internet


                    Administrator
                          |
                          v
                    Azure Bastion
                          |
                          v
                     Private VMs

```

🎓 AZ-104 Preparation

This repository is part of my practical preparation for:

Microsoft Certified: Azure Administrator Associate (AZ-104)

The objective is to combine certification preparation with hands-on Azure administration experience.

Rather than only studying individual services, I am building complete environments and validating how the services work together.

🚀 Lab Progress

| Lab    | Topic                             | Status      |
| ------ | --------------------------------- | ----------- |
| Lab 01 | 3-Tier Networking + Load Balancer | ✅ Completed |
| Lab 02 | Application Gateway               | 🔲 Planned  |
| Lab 03 | Azure Firewall + UDR              | 🔲 Planned  |
| Lab 04 | VNet Peering + VPN Gateway        | 🔲 Planned  |


📚 Networking Concepts Covered

| Topic               | Practical Focus                           |
| ------------------- | ----------------------------------------- |
| Virtual Networks    | VNet design, address spaces and subnets   |
| NSG                 | Inbound/outbound traffic control          |
| ASG                 | Application-based network security        |
| Load Balancer       | Layer 4 traffic distribution              |
| Application Gateway | Layer 7 application traffic management    |
| Front Door          | Global HTTP/HTTPS application delivery    |
| Azure DNS           | Public DNS resolution                     |
| Private DNS         | Private name resolution                   |
| Azure Firewall      | Centralized network security              |
| Route Tables / UDR  | Custom traffic routing                    |
| VNet Peering        | VNet-to-VNet connectivity                 |
| VPN Gateway         | Secure connectivity between networks      |
| ExpressRoute        | Private connectivity to Azure             |
| NAT Gateway         | Controlled outbound internet connectivity |



👨‍💻 Author - Sandeep Kadapa | Azure | Cloud | IAM | ITIL |
