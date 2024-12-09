# Fedora CoreOS pihole podman install

## Butane

```
butane --pretty --strict server-pihole.bu.yaml > server-pihole.ign.json
```

## coreos-installer
```
coreos-installer iso customize --dest-ignition "server-pihole.ign.json" --dest-device "/dev/sda" -o "fcos-datapihole-1.iso" "fedora-coreos-41.20241027.3.0-live.x86_64.iso"
```
