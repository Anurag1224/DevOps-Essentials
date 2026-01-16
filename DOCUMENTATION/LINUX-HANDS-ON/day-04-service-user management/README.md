# DevOps-Essentials: Day 4 - Service User Account Creation

## Task Overview
Create a system service user account named `rose` on App Server 2 without a home directory, as required by xFusionCorp Industries following a new tool implementation.

## Objective
Provision a service user account with specific constraints for application server environments.

## Requirements
- **Username**: rose
- **Server**: App Server 2
- **Home Directory**: None (disabled)
- **Purpose**: Service account for tool integration at xFusionCorp Industries

## Prerequisites
- Access to App Server 2 infrastructure
- Administrative/sudo privileges
- Knowledge of user account creation in Linux/Unix systems
- Reference to infrastructure details available in the KodeKloud platform

## Key Concepts
- Service user accounts (non-login users)
- User creation without home directory
- Linux `useradd` command with `-M` flag (no home directory)
- System administration basics

## Learning Outcomes
- Understanding service account creation
- Linux user management fundamentals
- Infrastructure navigation and documentation
- DevOps best practices for system configuration

## Related Resources
- [KodeKloud Engineer - Nautilus Project Infrastructure Details](https://kodekloudhub.github.io/kodekloud-engineer/docs/projects/nautilus#infrastructure-details)
- Linux `useradd` and `userdel` commands
- Service account management best practices

## Revision Notes
This task demonstrates practical implementation of Linux user management in a multi-server environment, critical for DevOps professionals managing application infrastructure.