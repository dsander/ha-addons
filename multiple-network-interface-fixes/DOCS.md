# Multiple Network Interface Fixes Add-on for Home Assistant

This Home Assistant add-on addresses issues with **excessive network activity** caused by mDNS name collisions, especially in environments with mDNS reflectors or multi-VLAN setups. In such networks, mDNS packets can be reflected across VLANs, causing name collisions and excessive mDNS traffic. It also ensure that the outgoing traffic of the Home Assistant uses the primary network connection.

## What This Add-on Does

- **Disables IPv4 gateway, DNS, and mDNS** on all active network connections except the user-specified "primary" connection and the loopback interface (`lo`).
- **Runs continuously** and checks connections at a configurable interval (default: 60 seconds).

## Why Use This Add-on?

- Prevents mDNS name collisions and excessive traffic in complex network setups.
- Ensures Home Assistant's network configuration remains stable, even if the Supervisor resets network settings.

## How It Works

1. **Primary Connection:**
   The add-on requires you to specify a "primary" network connection (e.g., `Supervisor enp1s0`). This is the only connection where mDNS and other network features are preserved.

2. **Other Connections:**
   All other active connections (except `lo`) have their IPv4 gateway, DNS, and mDNS disabled using `nmcli`.

## Example Configuration

```yaml
primary_connection: "Supervisor enp1s0"
sleep_time_seconds: 60
```

## Requirements

- Home Assistant OS or Supervised installation using **NetworkManager**
- `nmcli` available in the add-on container

## Disclaimer

This add-on is provided as-is and was developed to solve a specific issue in certain Home Assistant setups. It may not work for all configurations or network environments. Use at your own risk.

- Always back up your Home Assistant configuration before installing or modifying add-ons.
- This add-on modifies network settings; ensure you understand the implications for your network setup.

## Credits

This add-on was inspired by the [Network Manager Fix Add-on](https://github.com/sle118/addons-network-manager-fix/blob/main/network-manager-fix/DOCS.md).
