# Azure Networking Lab 2 — Azure Application Gateway with Path-Based Routing

## Overview

This lab demonstrates the implementation of an Azure Application Gateway
with path-based routing in a practical Azure network environment.

The objective was to deploy private Web and Application backend VMs,
provide secure management access using Azure Bastion, provide outbound
internet connectivity using Azure NAT Gateway, and expose the backend
applications through an Azure Application Gateway.

The Application Gateway was configured with:

- Public frontend IP
- HTTP listener
- Web backend pool
- Application backend pool
- Backend health monitoring
- Path-based routing
- Backend path override

The lab also included health-probe failure testing and troubleshooting
of backend path handling.

## Objectives

- Deploy a segmented Azure VNet
- Deploy private Web and Application VMs
- Configure Azure Bastion for management access
- Configure NAT Gateway for outbound internet connectivity
- Deploy Azure Application Gateway Standard V2
- Configure backend pools
- Configure HTTP listener
- Configure path-based routing
- Validate backend health
- Test backend failure detection
- Troubleshoot backend path routing