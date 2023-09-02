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
