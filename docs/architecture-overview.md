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