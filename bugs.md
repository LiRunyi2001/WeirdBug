# Weird Bugs
This is a file taking notes of bugs I've met, and how to fix them.
Bugs are recorded in time order.

## Import Error of PyTorch
### Description
ImportError: /opt/conda/envs/stylegan3/lib/python3.9/site-packages/torch/lib/libtorch_cuda.so: undefined symbol: cusparseSpSM_analysis, version libcusparse.so.11
### How to fix it
1. Find where your libcusparse.so.11 is.
2. Get there, and check your library links. This error is mostly caused by linking libcusparse.so and libcusparse.so.11 to an older version of libcusparse library. Unlink old link and re-link them to newer version.
3. REMEMBER also re-link libcudart.so and libcudart.so.11.

## GPU usage
### Description
I've used `CUDA_VISIBLE_DEVICES='1,2'` to let `accelerate` use GPU id 1 and 2, however it still uses GPU 0.
### How to fix it
Write a config.yaml like this:
```
compute_environment: LOCAL_MACHINE
distributed_type: MULTI_GPU
fp16: true
machine_rank: 0
main_process_ip: null
main_process_port: null
main_training_function: main
num_machines: 1
num_processes: 1
```
Then command like this:
```
CUDA_VISIBLE_DEVICES=1,2 accelerate launch \
    --config_file config.yaml \
    main.py \
```
It will use GPU 1 and 2, instead of 0 (by default).
