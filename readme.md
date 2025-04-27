# Fedora CoreOS pihole podman install
Automated Pi-hole Deployment on Fedora CoreOS

This configuration file provides a fully automated setup for deploying Pi-hole on Fedora CoreOS (FCOS). It includes user creation, disk configuration, and containerized deployment of Pi-hole using systemd.

## Key Features

1. User Management
    - Creates necessary system users, including pihole, root, and a user with SSH key authentication.
    - Enables lingering for the pihole user.
2. Storage Configuration
    - Manages partitions for / and /var, preserving /var across reinstallations.
    - Uses xfs as the filesystem format and resizes partitions dynamically.
3. File and Directory Setup
    - Configures important system files:
        - pihole.conf: Network tweaks for unprivileged ports.
        - Pi-hole container environment and systemd configuration files.
        - Disables systemd-resolved DNSStubListener.
    - Creates directories for persistent Pi-hole data and container configurations with proper permissions.
4. Systemd Integration
    - Defines custom systemd unit files to:
    - Deploy and manage the Pi-hole container (pihole.container).
    - Install and configure qemu-guest-agent for virtualization support.

5. Environment Variables
    - Configurable runtime settings include:
        - $ENVIRONMENT: Deployment environment (default: live).
        - $BIND: Host binding address (default: 0.0.0.0).
        - $BASE_URL: Base URL for the Pi-hole server.
        - $APPEND_PORT: Whether to append ports to the base URL.

6. Custom Pi-hole Deployment
    - Deploys the Pi-hole container with:
        - Persistent volumes for data (/opt/pihole/etc-pihole and /opt/pihole/etc-dnsmasq.d).
        - Ports exposed for DNS (53), HTTP (80), and HTTPS (443).
        - Custom DNS and hostname configurations.


## Installation

Project depends also for following binaries: ```butane``` and ```coreos-installer```. 

### Butane

```
Step 1: Using butane, create ignition file
butane --pretty --strict server-pihole.bu.yaml > server-pihole.ign.json
```

### coreos-installer
```
# Step 1: Download the Fedora CoreOS ISO
coreos-installer download --stream stable --architecture x86_64 --format iso -o "fedora-coreos-live.x86_64.iso"

# Step 2: Customize the downloaded ISO with ignition file
coreos-installer iso customize --dest-ignition "config.ign.json" --dest-device "/dev/sda" -o "custom-fcos.iso" "fedora-coreos-live.x86_64.iso"

```
