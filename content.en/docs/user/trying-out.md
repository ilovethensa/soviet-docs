---
weight: 1
bookFlatSection: true
title: "Trying out"
---

# Trying Out Soviet

While it's not currently suitable for daily use, you can still try out Soviet by running it within a Docker container or through chroot/systemd-nspawn.

**Login for container:**
- Username: root
- Password: sovietlinux

## Using chroot/systemd-nspawn
**Prerequisites:**
- Systemd (required for systemd-nspawn, you can still use chroot)

To get started, follow these steps:

1. Download a testing release from our [Discord server](https://discord.gg/5RVsSEej8M) in the #testing-releases channel.

2. Unpack the downloaded release using the following command:
   ```bash
   tar -xf "/path/to/soviet.tar.gz"
   ```
3. If you're using systemd-nspawn, enter the container with the following command:
   ```bash
   systemd-nspawn -bD "/path/to/soviet"
   ```
   If you don't have systemd, you can use chroot instead:
   ```bash
   sudo chroot "/path/to/soviet"
   ```

## Using Docker/Podman
**Prerequisites:**
- Podman or Docker (Podman recommended)

### Running the Container:
>Note: If you want this container to preserve changes you've made, remove `--rm`.
```bash
docker/podman run -it --rm ghcr.io/soviet-linux/soviet:latest /bin/bash
```
