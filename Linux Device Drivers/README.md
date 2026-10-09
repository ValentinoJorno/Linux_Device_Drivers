# Linux Device Drivers — Source Code Collection

This repository contains the source code examples from the **O'Reilly Linux Device Drivers (LDD)** book series. It serves as a personal reference and structured archive for learning kernel development, writing module code, and understanding Linux subsystem architectures.

## 📂 Repository Structure

The repository is organized into chapters and driver types. Below is an overview of the primary directories and the driver concepts they cover:

### Core Concepts & Fundamentals
* **`misc-modules/`** – Introductory kernel modules demonstrating initialization, cleanup, and basic module parameters.
* **`scull/`** – Simple Character Utility for Loading Localities. A complete character driver that uses computer memory as a device.
* **`short/`** – Simple Hardware Operations and Raw Tricks. Demonstrates digital I/O port registration and hardware control.

### Advanced Subsystems & Hardware
* **`pci/`** – Implementation of PCI bus detection, configuration space access, and device driver registration.
* **`usb/`** – USB device drivers showcasing the USB request block (URB) lifecycle and interface handling.
* **`tty/`** – TTY device drivers detailing the line discipline and serial communication layer.
* **`sbull/`** – Simple Block Utility for Loading Localities. A RAM-disk based block device driver showing request queues.
* **`snull/`** – Simple Network Utility for Loading Localities. A network interface driver simulating packet transmission without physical hardware.

### Memory & System Integration
* **`allocator/`** – Code samples detailing page allocations, slab caches, and custom memory management.
* **`scullc/`** & **`scullp/`** – Variants of the memory-based character driver utilizing memory caches and full pages.
* **`sculld/`** – A device driver variation illustrating advanced direct memory access (DMA) mapping and cache coherency.

---

## 🛠️ Getting Started

### Prerequisites
To build and run these drivers, you need a Linux development environment with the core build essentials and kernel headers matching your running kernel:
```bash
sudo apt update && sudo apt install build-essential linux-headers-$(uname -r)
```

### Building the Drivers
Navigate to any individual driver subdirectory and compile the module using the provided Makefile:
```bash
cd scull
make
```

### Loading and Unloading Modules
Insert the compiled kernel module (`.ko`) into the running kernel:
```bash
sudo insmod scull.ko
```
Verify the driver loaded successfully by checking the kernel ring buffer:
```bash
dmesg | tail
```
To remove the module from the system:
```bash
sudo rmmod scull
```

---

## 📜 Attribution & License
The original source code belongs to the authors of **Linux Device Drivers** published by **O'Reilly Media**. 
* This repository is maintained for educational purposes and personal reference.
* Please refer to the original book text for comprehensive conceptual breakdowns of each driver implementation.
