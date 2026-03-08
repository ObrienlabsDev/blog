# Ubuntu installation

```
sudo ubuntu-drivers install
 sudo apt install net-tools
vi ~/.bashrc
 58  sudo apt install openjdk-25-jdk
   59  sudo apt install maven
```
## CUDA
On 14900k based RTX-A6000
https://docs.nvidia.com/cuda/cuda-installation-guide-linux/

```
lspci | grep -i nvidia
01:00.0 VGA compatible controller: NVIDIA Corporation GA102GL [RTX A6000] (rev a1)
01:00.1 Audio device: NVIDIA Corporation GA102 High Definition Audio Controller (rev a1)

hostnamectl
 Static hostname: 14900c
       Icon name: computer-desktop
         Chassis: desktop 🖥️
Operating System: Ubuntu 25.10                    
          Kernel: Linux 6.17.0-14-generic
    Architecture: x86-64
 Hardware Vendor: ASUS
  Hardware Model: ROG MAXIMUS Z790 HERO
Firmware Version: 1303
   Firmware Date: Wed 2023-08-02
    Firmware Age: 2y 7month 6d 

sudo apt install nvidia-cuda-toolkit

gcc --version
sudo apt install gcc

nvidia-smi
Sun Mar  8 16:15:28 2026       
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 590.48.01              Driver Version: 590.48.01      CUDA Version: 13.1     |
+-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA RTX A6000               Off |   00000000:01:00.0 Off |                  Off |
| 30%   46C    P8             17W /  300W |       1MiB /  49140MiB |      0%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+
```

https://developer.nvidia.com/cuda-downloads
