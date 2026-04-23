# Linux Boot Process

The Linux boot process is a sequence of stages that the operating system follows from powering on the system until the user gets a login prompt. Understanding this process is crucial for system administrators and DevOps engineers when troubleshooting boot issues.

---

## Stages of Linux Boot Process

### 1. **BIOS/UEFI Initialization**

* When the computer is powered on, the **BIOS (Basic Input/Output System)** or **UEFI (Unified Extensible Firmware Interface)** initializes the hardware.
* Performs **POST (Power-On Self Test)** to check CPU, RAM, disk, and other components.
* Looks for a **bootable device** (HDD, SSD, CD/DVD, USB, or Network).

👉 Example:

* Pressing `F2` or `DEL` during boot enters the BIOS setup.
* Boot order can be configured to prioritize HDD or USB.

---

### 2. **MBR/GPT and Boot Loader**

* Once the boot device is found, BIOS/UEFI looks at the first sector of the disk:

  * **MBR (Master Boot Record)** for legacy systems (first 512 bytes).
  * **GPT (GUID Partition Table)** for modern systems.
* The boot loader is loaded from here. The most common boot loaders are:

  * **GRUB2** (GNU GRUB Boot Loader)
  * **LILO** (older Linux Loader)

👉 Example:

* GRUB menu appears allowing selection of kernels:

  ```
  Ubuntu
  Advanced options for Ubuntu
  Memory test (memtest86+)
  ```

---

### 3. **Kernel Loading**

* Boot loader loads the **Linux Kernel** into memory.
* Kernel is usually stored in `/boot/vmlinuz-*`.
* Kernel initializes hardware, mounts the root filesystem, and loads **initramfs** (temporary root filesystem).

👉 Example:

```bash
ls /boot
vmlinuz-5.15.0-25-generic  initrd.img-5.15.0-25-generic  grub/
```

---

### 4. **Initramfs and Hardware Detection**

* `initramfs` provides necessary drivers and modules required to mount the actual root filesystem.
* Once the root filesystem is mounted, control is transferred to the `init` system.

👉 Example:

```bash
lsinitramfs /boot/initrd.img-$(uname -r) | less
```

---

### 5. **Init/Systemd Process**

* Historically, **`/sbin/init`** was the first user-space program (PID 1).
* Most modern Linux distributions use **systemd** instead of init.
* It reads configuration files (like `/etc/systemd/system/*.service`) and starts system services.

👉 Example:

```bash
ps -p 1 -o comm=
# Output:
systemd
```

---

### 6. **Runlevels/Targets**

* The init/systemd process brings the system to a specific state:

  * Runlevel 0 → Halt
  * Runlevel 1 → Single-user mode
  * Runlevel 3 → Multi-user mode (CLI)
  * Runlevel 5 → Multi-user mode (GUI)
  * Runlevel 6 → Reboot
* In **systemd**, these are replaced by **targets**:

  * `poweroff.target`
  * `rescue.target`
  * `multi-user.target`
  * `graphical.target`
  * `reboot.target`

👉 Example:

```bash
systemctl get-default
# Output:
graphical.target
```

---

### 7. **Login Prompt**

* Once all required services are up, the system presents:

  * **TTY login prompt** (CLI mode)
  * **Display manager** (GUI mode, e.g., GDM, LightDM)

👉 Example:

```bash
# Switch to text-based login
Ctrl + Alt + F3
```

---

## Summary of Boot Process

```
BIOS/UEFI → MBR/GPT → Boot Loader (GRUB) → Kernel → Initramfs → Init/Systemd → Runlevel/Target → Login
```

---

## Troubleshooting Boot Issues

* **GRUB Rescue Mode**: Appears if GRUB configuration is broken.
* **Kernel Panic**: Happens when the kernel cannot mount root filesystem.
* **Systemd Failed Services**: Use `systemctl status` to debug.

👉 Example:

```bash
systemctl --failed
```

---

## Practical Example of Boot Logs

You can check the boot logs using:

```bash
journalctl -b
```

Or to see previous boots:

```bash
journalctl --list-boots
```

---


