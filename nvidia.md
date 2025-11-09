## NVIDIA GB10 Arm64 DGX Spark CUDA 13 - 10p10e

- https://github.com/ObrienlabsDev/performance/issues/45
- https://github.com/ObrienlabsDev/machine-learning/issues/47
- https://github.com/ObrienlabsDev/machine-learning/issues/48
- https://github.com/ObrienlabsDev/machine-learning/issues/49
- https://github.com/ObrienlabsDev/blog/blob/main/nvidia.md
- https://github.com/ObrienlabsDev/blog/issues/144
- https://github.com/NVIDIA/dgx-spark-playbooks
- 
- 20251108
- 202510 https://marketplace.nvidia.com/en-us/developer/dgx-spark
- https://www.canadacomputers.com/en/workstations/279129/nvidia-dgx-spark-ai-mini-pc-940-54242-0000-000-940-54242-0000-000.html?srsltid=AfmBOoqBukUC7jk2tNZSeKghJ-I4_1RjpcxHzvZKQrZ_y6Zv99z1FThQ
- https://www.youtube.com/watch?v=AvgZscNZzYw&t=105s

### nvidia-smi
```
michael@spark-7d19:~$ nvidia-smi
Sun Nov  9 09:26:12 2025       
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 580.95.05              Driver Version: 580.95.05      CUDA Version: 13.0     |
+-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GB10                    On  |   0000000F:01:00.0  On |                  N/A |
| N/A   45C    P0             11W /  N/A  | Not Supported          |     10%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI              PID   Type   Process name                        GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|    0   N/A  N/A            4174      G   /usr/lib/xorg/Xorg                       84MiB |
|    0   N/A  N/A            4399      G   /usr/bin/gnome-shell                    125MiB |
|    0   N/A  N/A            4761      G   .../7182/usr/lib/firefox/firefox        273MiB |
+-----------------------------------------------------------------------------------------+

michael@spark-7d19:~$ free
               total        used        free      shared  buff/cache   available
Mem:       125513720     5088412   118621120       20596     2728844   120425308
Swap:       16777212           0    16777212
michael@spark-7d19:~$ lscpu
Architecture:             aarch64
  CPU op-mode(s):         64-bit
  Byte Order:             Little Endian
CPU(s):                   20
  On-line CPU(s) list:    0-19
Vendor ID:                ARM
  Model name:             Cortex-X925
    Model:                1
    Thread(s) per core:   1
    Core(s) per socket:   10
    Socket(s):            1
    Stepping:             r0p1
    CPU(s) scaling MHz:   93%
    CPU max MHz:          4004.0000
    CPU min MHz:          1378.0000
    BogoMIPS:             2000.00
    Flags:                fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm jscvt fcma lrcpc dcpop sha3 sm3 sm4 asimddp sha512 sve asimdfhm dit uscat ilrcpc flagm sb paca pacg dcpodp sve2 sveaes svepmull sv
                          ebitperm svesha3 svesm4 flagm2 frint svei8mm svebf16 i8mm bf16 dgh bti ecv afp wfxt
  Model name:             Cortex-A725
    Model:                1
    Thread(s) per core:   1
    Core(s) per socket:   10
    Socket(s):            1
    Stepping:             r0p1
    CPU(s) scaling MHz:   112%
    CPU max MHz:          2860.0000
    CPU min MHz:          338.0000
    BogoMIPS:             2000.00
    Flags:                fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm jscvt fcma lrcpc dcpop sha3 sm3 sm4 asimddp sha512 sve asimdfhm dit uscat ilrcpc flagm sb paca pacg dcpodp sve2 sveaes svepmull sv
                          ebitperm svesha3 svesm4 flagm2 frint svei8mm svebf16 i8mm bf16 dgh bti ecv afp wfxt
Caches (sum of all):      
  L1d:                    1.3 MiB (20 instances)
  L1i:                    1.3 MiB (20 instances)
  L2:                     25 MiB (20 instances)
  L3:                     24 MiB (2 instances)
NUMA:                     
  NUMA node(s):           1
  NUMA node0 CPU(s):      0-19
Vulnerabilities:          
  Gather data sampling:   Not affected
  Itlb multihit:          Not affected
  L1tf:                   Not affected
  Mds:                    Not affected
  Meltdown:               Not affected
  Mmio stale data:        Not affected
  Reg file data sampling: Not affected
  Retbleed:               Not affected
  Spec rstack overflow:   Not affected
  Spec store bypass:      Mitigation; Speculative Store Bypass disabled via prctl
  Spectre v1:             Mitigation; __user pointer sanitization
  Spectre v2:             Not affected
  Srbds:                  Not affected
  Tsx async abort:        Not affected
```

### Upgrade Java on NVIDIA DGX Spark
- https://github.com/ObrienlabsDev/blog/issues/144
Install Java 25 with javac over the default 1.8 jre
```
git clone git@github.com:ObrienlabsDev/performance.git

sudo apt install maven

michael@spark-7d19:~$ java -version
openjdk version "1.8.0_462"
OpenJDK Runtime Environment (build 1.8.0_462-8u462-ga~us1-0ubuntu2~24.04.2-b08)
OpenJDK 64-Bit Server VM (build 25.462-b08, mixed mode)

michael@spark-7d19:~/wse_github/ObrienlabsDev/performance/cpu/virtual/multithreaded/128bit/java-benchmark-128-cli$ sudo apt install openjdk-25-jdk-headless
michael@spark-7d19:~/wse_github/ObrienlabsDev/performance/cpu/virtual/multithreaded/128bit/java-benchmark-128-cli$ javac -version
javac 25
michael@spark-7d19:~/wse_github/ObrienlabsDev/performance/cpu/virtual/multithreaded/128bit/java-benchmark-128-cli$ java -version
openjdk version "25" 2025-09-16
OpenJDK Runtime Environment (build 25+36-Ubuntu-124.04.2)
OpenJDK 64-Bit Server VM (build 25+36-Ubuntu-124.04.2, mixed mode, sharing)
```

### PyTorch on GB10 via docker
- https://github.com/ObrienlabsDev/machine-learning/issues/49
```
(venv-t214) michael@spark-7d19:~/wse_github/ObrienlabsDev/machine-learning$ sudo docker pull nvcr.io/nvidia/pytorch:25.09-py3
25.09-py3: Pulling from nvidia/pytorch
cc43ec4c1381: Pull complete 
...
216cdf20f351: Pull complete 
Digest: sha256:f3b4a33fd60d5e0358287bb44d57e91eda45e8f1681fef1bfd6c969371417130
Status: Downloaded newer image for nvcr.io/nvidia/pytorch:25.09-py3
nvcr.io/nvidia/pytorch:25.09-py3
(venv-t214) michael@spark-7d19:~/wse_github/ObrienlabsDev/machine-learning$ sudo docker run --gpus all -it --rm --ipc=host nvcr.io/nvidia/pytorch:25.09-py3
== PyTorch ==
NVIDIA Release 25.09 (build 210907838)
PyTorch Version 2.9.0a0+50eac81
Container image Copyright (c) 2025, NVIDIA CORPORATION & AFFILIATES. All rights reserved.
Copyright (c) 2014-2024 Facebook Inc.

root@c8522e0e1502:/workspace# vi pytorch.py

import torch
import os

print("cpus: ", os.cpu_count())

print("Torch:", torch.__version__)
print("CUDA:", torch.version.cuda)
print("GPU available:", torch.cuda.is_available())
print("GPU:", torch.cuda.get_device_name(0))

root@c8522e0e1502:/workspace# python pytorch.py 
/usr/local/lib/python3.12/dist-packages/torch/cuda/__init__.py:63: FutureWarning: The pynvml package is deprecated. Please install nvidia-ml-py instead. If you did not install pynvml directly, please report this to the maintainers of the package that installed pynvml for you.
  import pynvml  # type: ignore[import]
cpus:  20
Torch: 2.9.0a0+50eac811a6.nv25.09
CUDA: 13.0
GPU available: True
GPU: NVIDIA GB10
```
