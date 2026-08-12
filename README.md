# Linux Server Administration Lab

A hands-on Linux server administration project focused on building practical
skills required for IT Support and Linux System Administration roles.

The project is built progressively, starting from Linux fundamentals and
moving toward deploying and maintaining a real web application.

## Project Goals

- Manage Linux users and groups
- Understand Linux permissions and ownership
- Manage processes and system services
- Configure SSH access
- Configure and troubleshoot UFW firewall
- Troubleshoot networking and connectivity
- Deploy a Node.js application
- Manage PostgreSQL
- Configure Nginx as a reverse proxy
- Manage applications with systemd
- Analyze logs and troubleshoot failures
- Create backups
- Monitor server health

## Current Progress

Completed:

- System information
- User management
- Group management
- sudo privileges
- File ownership
- Linux permissions
- Process management
- systemd services
- journalctl logs
- SSH configuration
- SSH authentication
- SSH public key authentication
- SSH permissions
- SSH troubleshooting
- UFW firewall
- Firewall rules
- Network interfaces
- Ports and listening services
- `ss`
- Basic DNS troubleshooting
- Service and network troubleshooting

## Technologies

- Linux / Ubuntu
- Bash
- SSH
- systemd
- journalctl
- UFW
- Networking
- PostgreSQL
- Node.js
- Nginx
- Git

## Architecture

The final project will evolve toward:

Client
   |
   v
Nginx
   |
   v
Node.js Application
   |
   v
PostgreSQL

The server will be managed using:

- SSH
- systemd
- UFW
- journalctl
- Linux permissions
- monitoring and troubleshooting tools

## Troubleshooting Approach

The project focuses on diagnosing problems instead of blindly applying commands.

My troubleshooting process is:

1. Identify the symptoms
2. Gather information
3. Check possible causes
4. Test each hypothesis
5. Identify the root cause
6. Apply the fix
7. Verify the result
8. Document the solution

## Progress

- [x] Linux fundamentals
- [x] Users and groups
- [x] Permissions and ownership
- [x] Processes and services
- [x] SSH
- [x] Firewall
- [x] Basic networking
- [x] Troubleshooting
- [ ] PostgreSQL deployment
- [ ] Node.js deployment
- [ ] systemd application service
- [ ] Nginx reverse proxy
- [ ] Logging and monitoring
- [ ] Backups
- [ ] HTTPS
- [ ] Docker
- [ ] Docker Compose
- [ ] CI/CD
- [ ] Terraform

## Purpose

This is a hands-on learning project designed to develop practical Linux
administration, troubleshooting, and server management skills.
