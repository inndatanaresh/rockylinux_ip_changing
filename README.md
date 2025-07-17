# IP Address Configuration in Rocky Linux Using nmcli

This document provides the procedure to change or configure a static IP address on a Rocky Linux system using `nmcli` (NetworkManager Command Line Interface).

## Prerequisites

* Ensure you have root or sudo access.
* Identify the correct network interface (e.g., `ens18`).
* Backup existing network configuration if required.

## Step 1: Set Static IP Address

Modify the network connection to set a new static IP address:

```bash
sudo nmcli connection modify ens18 ipv4.addresses 10.10.5.70/24
```

## Step 2: Set Gateway

Configure the default gateway:

```bash
sudo nmcli connection modify ens18 ipv4.gateway 10.10.5.1
```

## Step 3: Set DNS Servers

Specify DNS servers:

```bash
sudo nmcli connection modify ens18 ipv4.dns "8.8.8.8 8.8.4.4"
```

## Step 4: Enable Manual IP Configuration

Ensure the IPv4 method is set to manual:

```bash
sudo nmcli connection modify ens18 ipv4.method manual
```

## Step 5: Apply the Changes

Bring the network connection down and back up to apply changes:

```bash
sudo nmcli connection down ens18
sudo nmcli connection up ens18
```

## Step 6: Verify IP Configuration

Check the updated IP address and configuration:

```bash
ip addr show ens18
```

---

**Notes:**

* Replace `ens18` with your actual network interface name if different.
* Ensure there are no conflicting DHCP settings.
* These changes persist across reboots.
