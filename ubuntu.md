# Ubuntu installation

past releases - https://releases.ubuntu.com/24.04/?C=S;O=D
- https://releases.ubuntu.com/24.04/ubuntu-24.04.5.1-desktop-amd64.iso
- https://releases.ubuntu.com/24.04/ubuntu-24.04.5-live-server-amd64.iso
- 

```
sudo ubuntu-drivers install
 sudo apt install net-tools
vi ~/.bashrc
 58  sudo apt install openjdk-25-jdk
   59  sudo apt install maven
```
## CUDA
- https://github.com/ObrienlabsDev/blog/blob/main/nvidia.md

### CUDA On 13900ks based dual RTX-A4500 with NVLink
- let ubuntu install drivers

```
sudo apt update
sudo apt install openssh-server

from other
ubuntu@13900ksd:~$ nvidia-smi
Wed Nov 18 20:58:12 2026       
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 595.99.02              Driver Version: 595.99.02      CUDA Version: 13.2     |
+-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA RTX A4500               Off |   00000000:01:00.0 Off |                  Off |
| 30%   36C    P8              5W /  200W |      15MiB /  20470MiB |      0%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+
|   1  NVIDIA RTX A4500               Off |   00000000:02:00.0 Off |                  Off |
| 30%   33C    P8             10W /  200W |      15MiB /  20470MiB |      0%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI              PID   Type   Process name                        GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|    0   N/A  N/A            3746      G   /usr/lib/xorg/Xorg                        4MiB |
|    1   N/A  N/A            3746      G   /usr/lib/xorg/Xorg                        4MiB |
+-----------------------------------------------------------------------------------------+

ubuntu@13900ksd:~$ nvcc
Command 'nvcc' not found, but can be installed with:
sudo apt install nvidia-cuda-toolkit
ubuntu@13900ksd:~$ sudo apt install nvidia-cuda-toolkit
[sudo] password for ubuntu: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu ca-certificates-java cpp-12 fonts-dejavu-extra g++-12 gcc-12 gcc-12-base java-common javascript-common libaccinj64-12.0 libamd-comgr2 libamdhip64-5 libasan8 libatk-wrapper-java
  libatk-wrapper-java-jni libbinutils libcc1-0 libctf-nobfd0 libctf0 libcu++-dev libcub-dev libcublas12 libcublaslt12 libcudart12 libcufft11 libcufftw11 libcuinj64-12.0 libcupti-dev libcupti-doc libcupti12 libcurand10 libcusolver11
  libcusolvermg11 libcusparse12 libgcc-12-dev libgl-dev libglx-dev libgprofng0 libhsa-runtime64-1 libhsakmt1 libhwloc-plugins libhwloc15 libibumad3 libitm1 libjpeg62 libjs-jquery libllvm17t64 liblsan0 libnppc12 libnppial12 libnppicc12
  libnppidei12 libnppif12 libnppig12 libnppim12 libnppist12 libnppisu12 libnppitc12 libnpps12 libnvblas12 libnvidia-ml-dev libnvjitlink12 libnvjpeg12 libnvrtc-builtins12.0 libnvrtc12 libnvtoolsext1 libnvvm4 libpfm4 libpthread-stubs0-dev
  libquadmath0 librdmacm1t64 libsframe1 libstdc++-12-dev libtbb-dev libtbb12 libtbbbind-2-5 libtbbmalloc2 libthrust-dev libtsan2 libubsan1 libucx0 libvdpau-dev libx11-dev libxau-dev libxcb1-dev libxdmcp-dev node-html5shiv nsight-compute
  nsight-compute-target nsight-systems nsight-systems-target nvidia-cuda-dev nvidia-cuda-gdb nvidia-cuda-toolkit-doc nvidia-opencl-dev nvidia-profiler nvidia-visual-profiler ocl-icd-opencl-dev opencl-c-headers opencl-clhpp-headers
  openjdk-8-jre openjdk-8-jre-headless x11proto-dev xorg-sgml-doctools xtrans-dev
Suggested packages:
  binutils-doc gprofng-gui gcc-12-locales cpp-12-doc g++-12-multilib gcc-12-doc gcc-12-multilib default-jre apache2 | lighttpd | httpd libhwloc-contrib-plugins libstdc++-12-doc libtbb-doc libvdpau-doc libx11-doc libxcb-doc nodejs
  nvidia-cuda-samples opencl-clhpp-headers-doc fonts-nanum fonts-ipafont-gothic fonts-ipafont-mincho fonts-wqy-microhei fonts-wqy-zenhei fonts-indic
Recommended packages:
  libnvcuvid1
The following NEW packages will be installed:
  binutils binutils-common binutils-x86-64-linux-gnu ca-certificates-java cpp-12 fonts-dejavu-extra g++-12 gcc-12 gcc-12-base java-common javascript-common libaccinj64-12.0 libamd-comgr2 libamdhip64-5 libasan8 libatk-wrapper-java
  libatk-wrapper-java-jni libbinutils libcc1-0 libctf-nobfd0 libctf0 libcu++-dev libcub-dev libcublas12 libcublaslt12 libcudart12 libcufft11 libcufftw11 libcuinj64-12.0 libcupti-dev libcupti-doc libcupti12 libcurand10 libcusolver11
  libcusolvermg11 libcusparse12 libgcc-12-dev libgl-dev libglx-dev libgprofng0 libhsa-runtime64-1 libhsakmt1 libhwloc-plugins libhwloc15 libibumad3 libitm1 libjpeg62 libjs-jquery libllvm17t64 liblsan0 libnppc12 libnppial12 libnppicc12
  libnppidei12 libnppif12 libnppig12 libnppim12 libnppist12 libnppisu12 libnppitc12 libnpps12 libnvblas12 libnvidia-ml-dev libnvjitlink12 libnvjpeg12 libnvrtc-builtins12.0 libnvrtc12 libnvtoolsext1 libnvvm4 libpfm4 libpthread-stubs0-dev
  libquadmath0 librdmacm1t64 libsframe1 libstdc++-12-dev libtbb-dev libtbb12 libtbbbind-2-5 libtbbmalloc2 libthrust-dev libtsan2 libubsan1 libucx0 libvdpau-dev libx11-dev libxau-dev libxcb1-dev libxdmcp-dev node-html5shiv nsight-compute
  nsight-compute-target nsight-systems nsight-systems-target nvidia-cuda-dev nvidia-cuda-gdb nvidia-cuda-toolkit nvidia-cuda-toolkit-doc nvidia-opencl-dev nvidia-profiler nvidia-visual-profiler ocl-icd-opencl-dev opencl-c-headers
  opencl-clhpp-headers openjdk-8-jre openjdk-8-jre-headless x11proto-dev xorg-sgml-doctools xtrans-dev
0 upgraded, 108 newly installed, 0 to remove and 70 not upgraded.
Need to get 2,300 MB of archives.
After this operation, 7,063 MB of additional disk space will be used.

ubuntu@13900ksd:~$ nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2023 NVIDIA Corporation
Built on Fri_Jan__6_16:45:21_PST_2023
Cuda compilation tools, release 12.0, V12.0.140
Build cuda_12.0.r12.0/compiler.32267302_0

```
### CUDA On 14900k based RTX-A6000
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
### CUDA Toolkit
https://developer.nvidia.com/cuda-downloads

```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-ubuntu2404.pin
sudo mv cuda-ubuntu2404.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/13.1.1/local_installers/cuda-repo-ubuntu2404-13-1-local_13.1.1-590.48.01-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2404-13-1-local_13.1.1-590.48.01-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2404-13-1-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda-toolkit-13-1

nvidia-smi
Sun Mar  8 16:22:04 2026       
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 590.48.01              Driver Version: 590.48.01      CUDA Version: 13.1     |
+-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA RTX A6000               Off |   00000000:01:00.0 Off |                  Off |
| 30%   49C    P8              7W /  300W |       1MiB /  49140MiB |      0%      Default |
|                                         |                        |                  N/A |
```

### Testing CUDA
- compile and run some of my CUDA code in https://github.com/ObrienlabsDev/fractals/blob/main/README.md#14900c-rtx-a6000-ubuntu
