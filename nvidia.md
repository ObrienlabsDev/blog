## NVIDIA GB10 Arm DGX Spark
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
```
