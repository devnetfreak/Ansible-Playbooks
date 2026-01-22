# FortiGate Backup Automation

Ansible playbook to backup FortiGate firewall configuration via REST API.

## Prerequisites

- Ansible 2.9+
- Python 3.6+
- Fortinet.fortios collection

## Installation

1. Install required collections:
   ```bash
   ansible-galaxy collection install -r requirements.yml
   ```

## Configuration

### Inventory
- **Host**: `fortigate_primary`
- **IP**: `10.0.80.1`
- **Port**: `9310` (HTTPS)
- **Location**: `inventory/hosts.yml`

### Credentials
- **API User**: `lakhi_api`
- **API Key**: Stored in `group_vars/fortigate.yml`

### Backup Location
- **Directory**: `/ansible/Backup/`
- **Filename Format**: `fortigate_<hostname>_<timestamp>.conf`

## Usage

Run backup playbook:
```bash
cd /ansible
ansible-playbook playbooks/backup_config.yml -i inventory/hosts.yml
```

Or with inventory inline:
```bash
ansible-playbook playbooks/backup_config.yml
```

## Output

Backups are saved to `/ansible/Backup/` with timestamp:
```
fortigate_fortigate_primary_20260120T1530.conf
```

## Notes

- SSL certificate validation is disabled (`ansible_httpapi_validate_certs: false`)
- Trusthost configuration should be set up in FortiGate GUI to restrict API access
- Default VDOM is used (root)
- Backup files are ready for restoration via FortiGate GUI

## Restoring from Backup

1. Log into FortiGate GUI
2. Go to **System** → **Configuration** → **Restore**
3. Upload the `.conf` file from `/ansible/Backup/`
4. Click **Restore**
