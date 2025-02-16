# Ansible Docker Deployment Project

Automated deployment of WordPress, MySQL, phpMyAdmin, and Nginx with SSL using Ansible and Docker Compose.

## Usage

### 1. Configure Inventory

Create an `inventory.yml` file:
```yaml
servers:
  hosts:
    debian1:
      ansible_host: # your remote server ip
      ansible_user: # your remote server user
```

### 2. Create Docker Secrets

⚠️ **IMPORTANT**: The project requires these secrets to work!

Create the following files in `docker-setup/secrets/`:
```bash
mkdir -p docker-setup/secrets/
echo "your-db-password" > docker-setup/secrets/db_password.txt
echo "your-root-password" > docker-setup/secrets/db_root_password.txt
```

### 3. Running the Project

To deploy:
```bash

# root user
ansible-playbook site.yml

# non-root user
ansible-playbook site.yml --ask-become-pass
```

To clean up:
```bash
# root user
ansible-playbook clean.yml

# non-root user
ansible-playbook clean.yml --ask-become-pass
```

## Project Structure

```
.
├── ansible.cfg
├── clean.yml                    # Cleanup playbook
├── site.yml                     # Main deployment playbook
├── docker-setup/
│   ├── compose.yml             # Docker compose configuration
│   └── nginx.conf              # Nginx reverse proxy configuration
└── roles/
    ├── cert_generation/        # SSL certificate generation
    ├── docker_setup/           # Docker installation and deployment
    └── env_cleaning/           # Environment cleanup
```

## Technologies

- **[Ansible](https://www.ansible.com/)**: Infrastructure automation
- **[Docker](https://www.docker.com/) & [Docker Compose](https://docs.docker.com/compose/)**: Container orchestration 
- **[Nginx](https://nginx.org/)**: Reverse proxy with SSL termination
- **[WordPress](https://wordpress.org/)**: Content management system
- **[MySQL](https://www.mysql.com/)**: Database server
- **[phpMyAdmin](https://www.phpmyadmin.net/)**: Database management interface
