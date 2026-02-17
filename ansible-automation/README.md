# Ansible Automation

Reusable Ansible roles for Docker, Docker Compose installation, and server patching.

## Directory Structure

```
ansible-automation/
├── ansible.cfg
├── requirements.yml
├── inventory/
│   └── hosts.yml
├── group_vars/
│   ├── all.yml
│   └── docker_hosts.yml
├── playbooks/
│   ├── docker.yml
│   ├── server-patching.yml
│   └── full-setup.yml
└── roles/
    ├── docker/
    ├── docker-compose/
    └── server-patching/
```

## Roles

### Docker Role
Installs Docker CE on Debian/Ubuntu and RedHat/CentOS systems.

**Variables:**
- `docker_users`: List of users to add to docker group
- `docker_daemon_options`: Docker daemon configuration

### Docker Compose Role
Installs Docker Compose plugin or standalone binary.

**Variables:**
- `docker_compose_version`: Version to install (standalone only)
- `docker_compose_standalone`: Use standalone binary instead of plugin

### Server Patching Role
Performs system updates with optional reboot.

**Variables:**
- `patching_reboot_enabled`: Enable automatic reboot if required
- `patching_security_only`: Install security updates only
- `patching_exclude_packages`: List of packages to exclude

## Usage

```bash
# Install dependencies
ansible-galaxy collection install -r requirements.yml

# Install Docker
ansible-playbook playbooks/docker.yml

# Patch servers
ansible-playbook playbooks/server-patching.yml

# Full setup (patching + Docker)
ansible-playbook playbooks/full-setup.yml

# Target specific hosts
ansible-playbook playbooks/docker.yml -l docker-server-1

# Dry run
ansible-playbook playbooks/server-patching.yml --check
```
