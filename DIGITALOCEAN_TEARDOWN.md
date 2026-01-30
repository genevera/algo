# DigitalOcean Teardown

This playbook destroys a DigitalOcean Algo VPN deployment and cleans up all associated resources.

## Prerequisites

- `config.cfg` with your DigitalOcean deployment settings (must have `algo_do_token` and `algo_server_name`)
- The `community.digitalocean` Ansible collection installed
- Python `requests` library (usually installed with community.digitalocean)

## Usage

```bash
ansible-playbook digitalocean-teardown.yml
```

## What Gets Deleted

1. **Droplet**: The main DigitalOcean droplet/instance
2. **Floating IP(s)**: Any floating IPs attached to the droplet (if Alternative Ingress IP was used)
3. **SSH Key**: The SSH key used for this specific deployment

## Important Notes

⚠️ **This action is irreversible!** Make sure you:
- Have backed up any important data from the server
- Are deleting the correct droplet
- Have the correct `algo_server_name` in your `config.cfg`

## Dry Run (Optional)

To see what would be deleted without actually deleting:

```bash
ansible-playbook digitalocean-teardown.yml --check
```

## Troubleshooting

**"No droplet named 'X' found"**
- The droplet may have already been deleted
- Check `algo_server_name` in `config.cfg` matches your droplet name

**Token authentication error**
- Ensure `algo_do_token` is set in `config.cfg`
- Verify the token is still valid in your DigitalOcean account

**SSH key not found**
- The SSH key may have been manually deleted from DigitalOcean
- The playbook will continue with other cleanup tasks
