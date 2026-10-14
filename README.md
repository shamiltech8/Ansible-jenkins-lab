# Ansible Automation with Jenkins CI/CD

A hands-on DevOps project demonstrating how Jenkins automates Ansible playbooks to inspect and verify an AWS EC2 server.

## Project Overview

This project integrates Jenkins, Ansible, SSH, and AWS EC2 to automate server checks and verify that a Docker Nginx container is running.

## Technology Stack

- Ansible
- Jenkins Pipeline
- AWS EC2
- Docker
- Nginx
- Git and GitHub
- SSH

## Architecture

GitHub → Jenkins Pipeline → Ansible → SSH → AWS EC2 → Docker Nginx

## Pipeline Stages

1. Check Git and Ansible tools.
2. Validate the local Ansible playbook.
3. Execute a local Ansible automation test.
4. Test SSH connectivity to EC2.
5. Inspect the EC2 hostname and operating system.
6. Verify the Docker Nginx container.
7. Create and verify an Ansible-managed configuration file.
8. Run the final server and application verification using reusable Ansible roles.

## Ansible Project Structure

```text
.
├── Jenkinsfile
├── README.md
├── inventory/
│   └── production.ini
├── roles/
│   ├── server_setup/
│   │   └── tasks/
│   │       └── main.yml
│   └── app_verify/
│       └── tasks/
│           └── main.yml
├── server-setup.yml
├── final-project-check.yml
├── ec2-playbook.yml
├── ec2-config-playbook.yml
└── playbook.yml
```

## Verification

The final Jenkins pipeline successfully verified:

- SSH connectivity to the EC2 server.
- Server hostname and available disk space.
- Docker Nginx container existence and running state.
- Ansible-managed configuration file contents.
- Reusable server configuration and application verification roles.

The final verification playbook completed with **7 successful tasks and 0 failures** in the recorded Jenkins run.

## Run the Final Verification Manually

From the project directory, with valid SSH access and the required Ansible collection installed:

```bash
ansible-playbook \
  -i inventory/production.ini \
  final-project-check.yml
```

## Security Notes

- Use Jenkins credentials for SSH private keys.
- Keep SSH host-key verification enabled.
- Never commit private keys, passwords, or other secrets.
- Restrict AWS security-group access to trusted sources.
- Review Ansible privilege escalation before running tasks with elevated permissions.

## Learning Outcomes

- Integrating Ansible with a Jenkins Pipeline.
- Managing EC2 servers over SSH.
- Organizing reusable Ansible roles and inventories.
- Automating Docker application verification.
- Validating and documenting a CI/CD workflow.
