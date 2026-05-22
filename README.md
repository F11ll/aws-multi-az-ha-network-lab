# AWS Multi-AZ High Availability Network Lab

Designed and implemented a highly available AWS network architecture across two Availability Zones with secure private workloads, bastion-based administration, outbound internet access using NAT, and failover validation using an Application Load Balancer.

---

## Architecture Overview

- 1 VPC
- 2 Availability Zones
- 2 Public Subnets
- 2 Private Subnets
- Bastion Host
- NAT Instance
- 2 Private Application Servers
- Application Load Balancer
- Target Group + Health Checks
- Security Groups + Route Tables

---

## Architecture

Internet
   │
   ▼
Application Load Balancer
   │
   ├── App-01 (Private / AZ1)
   └── App-02 (Private / AZ2)

Bastion Host (Public)
   │
   ├── SSH → App-01
   └── SSH → App-02

NAT Instance (Public)
   │
   ├── Private AZ1 outbound
   └── Private AZ2 outbound
```

---

## Security Validation

Private instances reject direct SSH access from the internet.

![Private Security](assets/00-private-security.png)

---

## Infrastructure Validation

![Instances](assets/01-instances.png)

![Security Groups](assets/02-security-groups.png)

![Internet Gateway](assets/03-internet-gateway.png)

![Load Balancer](assets/04-load-balancer.png)

![Target Group](assets/05-target-group.png)

![Resource Map](assets/06-resource-map.png)

---

## Secure Administration

SSH access to private workloads is allowed only through the Bastion Host.

![Bastion Access](assets/07-ssh-bastion-host.png)

---

## Outbound Internet Access

Private workloads access the internet through the NAT instance.

![App Using NAT](assets/08-app-using-nat.png)

![NAT Instance](assets/09-nat-instance.png)

---

## Application Validation

App server in AZ1:

![App 01](assets/10-app-01.png)

App server in AZ2:

![App 02](assets/11-app-02.png)

---

## High Availability Testing

Failover validation after stopping one application instance:

![Failover Test](assets/12-failover-test.png)

---

## Recovery Validation

Health checks recovered after restoring the failed instance:

![Recovery](assets/13-recovery.png)

---

## Skills Demonstrated

- AWS VPC Design
- Public / Private Networking
- Security Groups
- Route Tables
- Bastion Architecture
- NAT Configuration
- Application Load Balancing
- Health Checks
- Multi-AZ Failover Testing
- Linux Administration
- SSH Troubleshooting





## Design Note
This lab uses a single NAT instance in Public Subnet AZ1 for cost optimization.
In production, use one NAT Gateway per AZ.

