# 20261115: CUDA warp in SIMT lockstep allows for branches where all 32 threads act as single processors - allowing for MIMD
Use either FP32, INT32 for integer math.
For example the RTX-3500 Ada AD104 CC8.9 had 5120 CIDA cores, 1920 max warps and 61440 concurrent threads
Thread blocks per SM = 24

threads group into blocks
threads group into warps of 32 = SIMT
Blocks are assigned to SMs (Streaming Multiprocessors)


Check the 160 tensor cores for INT4/INT8/FP8
