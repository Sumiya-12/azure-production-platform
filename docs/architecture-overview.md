# Architecture Overview

## Current State
The environment currently includes:
- 1 resource group
- 1 virtual network
- multiple subnets
- web VM
- app VM
- NSG rules for controlled access

## Purpose
This setup is the foundation for a multi-tier Azure architecture.

## Why this matters
This project is being expanded step by step to cover:
- Azure administration tasks
- production design concepts
- architect-level decision making

### Subnets:
- subnet-web -> 10.1.1.0/24
- subnet-app -> 10.1.2.0/24
- subnet-mgmt -> 10.1.3.0/24

## NSG Rules

### nsg-web
- Allow inbound HTTP (80) from Internet
- Allow inbound HTTPS (443) from Internet

### nsg-app
- Allow inbound TCP 8080 from subnet-web (10.1.1.0/24)

### nsg-mgmt
- Allow inbound SSH (22) only from my public IP

## Validation Results

- vm-web-01 is reachable from the internet over HTTP
- vm-app-01 has no public IP, so it is not directly accessible from the internet
- This supports a layered architecture where the app tier remains private

- vm-web-01 is reachable from the internet over HTTP
- Direct SSH access to the web subnet is blocked because nsg-web does not allow port 22
- This supports a more secure design where web traffic is public but administrative access is separated

## Management Tier

- Added vm-mgmt-01 in subnet-mgmt
- Used Standard_D2s_v3 due to regional SKU availability
- Management VM is the secure administrative entry point for the environment

## Final Network Behavior

- Internet access is allowed only to the web tier (HTTP/HTTPS)
- App tier is fully private with no public exposure
- Administrative access is routed through vm-mgmt-01
- Internal communication:
  - Mgmt → Web/App over SSH (22)
  - Web → App over application port (8080)
- Direct SSH from internet to web/app is blocked

## Exposure Review

- vm-web-01 has a public IP and serves as the public web entry point
- vm-app-01 has no public IP and remains private
- vm-mgmt-01 has a public IP and serves as the controlled administrative entry point