# Scull Driver Project

This folder contains the source code for the Linux scull driver.

* For the main driver documentation, see [README.md](README.md).
* For details on the initialization script, see the [Scull Init Documentation](INIT_GUIDE.md).

# SCULL Character Device Driver

A Linux kernel character device driver based on the
**SCULL (Simple Character Utility for Loading Localities)** 
example from the classic book *Linux Device Drivers (3rd Edition)*. 
This repository serves as an educational project to understand Linux kernel internals, 
memory allocation, and character device management.

## 🚀 Features
- **In-memory storage**: Simulates a device by allocating memory chunks dynamically using `kmalloc`.
- **Character device operations**: Implements standard file operations including `open`, `release`, `read`, `write`, and `llseek`.
- **Dynamic & Static Quantum Allocation**: Manages data memory using a quantum-set linked list structure.
- **Dynamic Major Number Allocation**: Automatically requests an available major number from the kernel.

## 🛠️ Prerequisites
To build and run this kernel module, you will need:
- A Linux environment (Ubuntu/Debian recommended).
- Essential build tools and kernel headers. Install them using:
  ```bash
  sudo apt update
  sudo apt install build-essential linux-headers-$(uname -r)
  ```

## 📦 Compilation
Clone the repository and build the kernel module using the provided `Makefile`:

```bash
git clone https://github.com/ValentinoJorno/Linux_Device_Drivers.git
cd YOUR_REPO_NAME
make
```
This will generate the kernel object file: `scull.ko`.

## ⚙️ Loading and Unloading
You can load the module into the kernel and check its status using the following steps.

### 1. Load the module
```bash
sudo insmod scull.ko
```

### 2. Verify it is loaded
Check if the module appears in the kernel list and verify its major number assignment:
```bash
lsmod | grep scull
cat /proc/devices | grep scull
```

### 3. Create the device node
Find the major number from `/proc/devices` (e.g., `240`) and create a device node in `/dev`:
```bash
sudo mknod /dev/scull0 c 240 0
sudo chmod 666 /dev/scull0
```

### 4. Unload the module
To clean up and remove the module:
```bash
sudo rmmod scull
sudo rm /dev/scull0
```

## 🧪 Testing the Driver
Once the device node `/dev/scull0` is created, you can interact with it using basic shell commands:

**Write data to the device:**
```bash
echo "Hello from user space!" > /dev/scull0
```

**Read data back from the device:**
```bash
cat /dev/scull0
```

**Check kernel log outputs:**
```bash
dmesg | tail -n 20
```

## 🧼 Cleanup
To remove all generated build files, run:
```bash
make clean
```

## 📚 References
- *Linux Device Drivers, 3rd Edition* (LDD3) by Jonathan Corbet, Alessandro Rubini, and Greg Kroah-Hartman.

## 📄 License
This project is licensed under the GPL-2.0 License - see the LICENSE file for details.
