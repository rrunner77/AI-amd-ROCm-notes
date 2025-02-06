# AI-amd-ROCm-notes
my notes to ROCm, WLS2, Stable Diffusion, xformers

Installation of Automatic1111 with ROCm on a WSL2 Windows 11 - for now no xformers

1. You need to have WSL2 on Windows 11
2. install python 3.10.16 - I installed from deadsnakes
3. install ROCm -> https://rocm.docs.amd.com/projects/radeon/en/latest/docs/install/wsl/install-radeon.html
4. You need to restart the WLS2 it is said on the page but it seems to work without it also
5. git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui
6. cd stable-diffusion-webui
7. python -m venv venv
8. source venv/bin/activate
9. python -m pip install --upgrade pip wheel
10. TORCH_COMMAND='pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/rocm6.3/' python launch.py --precision full --no-half --skip-torch-cuda-test
11. It will not work but install all the prerequisites. 
12. You need to copy the ROCm to the venv environment: https://rocm.docs.amd.com/projects/radeon/en/latest/docs/install/wsl/install-pytorch.html -> point 4
13. cp /opt/rocm/lib/libhsa-runtime64.so.1.14.0 venv/lib/python3.10/site-packages/torch/lib/libhsa-runtime64.so
14. cp /opt/rocm/lib/libhsa-runtime64.so.1.14.0 venv/lib/python3.10/site-packages/triton/backends/amd/lib/libhsa-runtime64.so
15. cd stable-diffusion-webui
16. source venv/bin/activate
17. TORCH_COMMAND='pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/rocm6.3/' python launch.py --precision full --no-half
