
# Install Kali Linux and Nvidia-drivers

This is for users who want to install Kali Linux but encounter problems during installation where the user cannot install xfce or gnome. And for people who have Nvidia cards but are still using Nouveau drivers.





## Installation of Kali via CLI

Update system

```bash
  sudo apt update
  sudo apt upgrade
```

If running into networking problems try:

```bash
  sudo dhclient
```

Install Nvidia-drivers

```bash
kali@kali:~$ lspci | grep -i vga
07:00.0 VGA compatible controller: NVIDIA Corporation GP106 [GeForce GTX 1060 6GB] (rev a1)
kali@kali:~$
kali@kali:~$ lspci -s 07:00.0 -v
07:00.0 VGA compatible controller: NVIDIA Corporation GP106 [GeForce GTX 1060 6GB] (rev a1) (prog-if 00 [VGA controller])
        Subsystem: Gigabyte Technology Co., Ltd GP106 [GeForce GTX 1060 6GB]
        Flags: bus master, fast devsel, latency 0, IRQ 100
        Memory at f6000000 (32-bit, non-prefetchable) [size=16M]
        Memory at e0000000 (64-bit, prefetchable) [size=256M]
        Memory at f0000000 (64-bit, prefetchable) [size=32M]
        I/O ports at e000 [size=128]
        Expansion ROM at 000c0000 [disabled] [size=128K]
        Capabilities: <access denied>
        Kernel driver in use: nouveau
        Kernel modules: nouveau

kali@kali:~$
```

```bash
kali@kali:~$ sudo apt install -y nvidia-detect
[...]
kali@kali:~$ nvidia-detect
Detected NVIDIA GPUs:
01:00.0 3D controller [0302]: NVIDIA Corporation GM108M [GeForce 940MX] [10de:134d] (rev a2)

Checking card:  NVIDIA Corporation GM108M [GeForce 940MX] (rev a2)
Uh oh. Failed to identify your Debian suite.

kali@kali:~$
kali@kali:~$ lspci -s 01:00.0 -v
01:00.0 3D controller: NVIDIA Corporation GM108M [GeForce 940MX] (rev a2)
        Subsystem: Lenovo GM108M [GeForce 940MX]
        Flags: bus master, fast devsel, latency 0, IRQ 132, IOMMU group 10
        Memory at 93000000 (32-bit, non-prefetchable) [size=16M]
        Memory at 80000000 (64-bit, prefetchable) [size=256M]
        Memory at 90000000 (64-bit, prefetchable) [size=32M]
        I/O ports at 5000 [size=128]
        Capabilities: <access denied>
        Kernel driver in use: nouveau
        Kernel modules: nouveau
kali@kali:~$
```

```bash
kali@kali:~$ sudo apt install -y nvidia-driver nvidia-cuda-toolkit

┌─────────────────────────────────┤ Configuring xserver-xorg-video-nvidia ├─────────────────────────────────┐
│                                                                                                           │
│ Conflicting nouveau kernel module loaded                                                                  │
│                                                                                                           │
│ The free nouveau kernel module is currently loaded and conflicts with the non-free nvidia kernel module.  │
│                                                                                                           │
│ The easiest way to fix this is to reboot the machine once the installation has finished.                  │
│                                                                                                           │
│                                                  <Ok>                                                     │
│                                                                                                           │
└───────────────────────────────────────────────────────────────────────────────────────────────────────────┘

kali@kali:~$
kali@kali:~$ sudo reboot -f
kali@kali:~$
```

```bash
kali@kali:~$ nvidia-smi
Tue Jan 28 11:37:47 2020
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 430.64       Driver Version: 430.64       CUDA Version: 10.1     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 106...  Off  | 00000000:07:00.0  On |                  N/A |
|  0%   50C    P8     7W / 120W |    116MiB /  6075MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0       807      G   /usr/lib/xorg/Xorg                           112MiB |
|    0       979      G   xfwm4                                          2MiB |
+-----------------------------------------------------------------------------+
kali@kali:~$
kali@kali:~$ lspci | grep -i vga
07:00.0 VGA compatible controller: NVIDIA Corporation GP106 [GeForce GTX 1060 6GB] (rev a1)
kali@kali:~$
kali@kali:~$ lspci -s 07:00.0 -v
[...]
        Kernel driver in use: nvidia
        Kernel modules: nvidia

kali@kali:~$
```

Install kali-linux-gnome

```bash
  sudo apt-get update
  sudo apt-get install kali-desktop-gnome
  sudo reboot
```
