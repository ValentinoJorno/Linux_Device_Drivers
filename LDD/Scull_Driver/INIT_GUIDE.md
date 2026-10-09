# Scull Driver Initialization Script

A robust Bash initialization script designed to manage the lifecycle of the **scull** (Simple Character Utility for Loading Localities) kernel module. It automates loading the module, fetching its assigned major number, dynamically creating character device nodes in `/dev`, and cleaning them up upon unloading.

## Features

- **Automated Lifecycle Management:** Supports `start`, `stop`, `restart`, and `force-reload` commands.
- **Dynamic Device Creation:** Automatically reads `/proc/devices` to fetch the major number and creates specific device nodes (e.g., `scull0` to `scull3`, `scullpipe`, `scullsingle`).
- **Permissions Control:** Custom ownership, groups, and permissions can be applied via an external configuration file.
- **Pre/Post Hooks:** Includes customizable `device_specific_post_load` and `device_specific_pre_unload` functions for specialized setup.

## Prerequisites

- **Root Privileges:** Modifying kernel modules and `/dev` nodes requires root access.
- **Compiled Module:** The `scull.o` (or `scull.ko`) kernel module file must be available either in the current directory or the system module path (`/lib/modules/$(uname -r)/`).

## Configuration

You can optionally configure device ownership and permissions by creating a configuration file at `/etc/scull.conf`. 

### Example `/etc/scull.conf`
```text
owner root
group wheel
mode 660
options some_module_param=1
```

## Usage

Run the script as **root** or via `sudo` using one of the following arguments:

### Load the Driver and Create Nodes
```bash
sudo ./scull_init start
```

### Unload the Driver and Remove Nodes
```bash
sudo ./scull_init stop
```

### Restart / Reload the Driver
```bash
sudo ./scull_init restart
```

## Device Nodes Managed

The script creates and manages the following nodes under `/dev/`:
- `scull0`, `scull1`, `scull2`, `scull3` (Standard memory areas)
- `scullpriv` (Private per-process text area)
- `scullpipe0`, `scullpipe1`, `scullpipe2`, `scullpipe3` (FIFO pipes)
- `scullsingle` (Single-open device)
- `sculluid`, `scullwuid` (UID-restricted devices)

## Troubleshooting

- **"You must be root to load or unload kernel modules"**: Ensure you are running the script with `sudo` or as the root user.
- **FAILED!**: If loading fails, ensure the compiled module (`scull.ko` or `scull.o`) matches your current kernel version (`uname -r`) and is positioned correctly. Check `dmesg` for kernel logs.

## Credits
Original script skeleton by Alessandro Rubini `<rubini@linux.it>`.
