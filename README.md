Hi,
if anyone is interested to have stable diffusion on Windows with Ubuntu on WSL2. (Did not tested on unsupported cards by ROCm)
My config is:
AMD Ryzen 9900x
AMD RX7900XTX
RAM 64GB

1. Need to install on W11 the WSL2 Ubuntu(should be the 24.04 by default) - Should work via Microsoft store
    - wsl --install Ubuntu-24.04
    - if it works you need to enter first username and create password.
    - access to the disk inside he WSL is in explorere and from linux to windows disk through /mnt/c/
2. install python 3.10.16 - I installed from deadsnakes (installed all packgages like "sudo apt install python3.10*")
    - sudo add-apt-repository ppa:deadsnakes/ppa  - or if you are too scared to use this repo you can compile from source.
    - sudo apt install python3.10*
3. install ROCm -> https://rocm.docs.amd.com/projects/radeon/en/latest/docs/install/wsl/install-radeon.html - I have tested only the latest version of ROCm 6.3.2
4. wget https://repo.radeon.com/amdgpu-install/6.3.2/ubuntu/noble/amdgpu-install_6.3.60302-1_all.deb
    - sudo apt install ./amdgpu-install_6.3.60302-1_all.deb
    - sudo amdgpu-install --list-usecase
    - amdgpu-install -y --usecase=wsl,rocm --no-dkms
    - to check if it is working: "rocminfo"
    - You need to restart the WLS2 -> "sudo reboot"
5. cd ~
6. git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui
7. cd stable-diffusion-webui
8. python3.10 -m venv venv
9. source venv/bin/activate
10. python3.10 -m pip install --upgrade pip wheel
11. pip3.10 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/rocm6.3/
12. Optional as A1111 does not work with xformers for ROCm -> pip3.10 install -v -U git+https://github.com/facebookresearch/xformers.git@main#egg=xformers
      - you can test xformers by "python -m xformers.info"

pip3.10 install -v -U git+https://github.com/ROCm/xformers@for_upstream - from ROCm page

13. cp /opt/rocm/lib/libhsa-runtime64.so.1.14.0 venv/lib/python3.10/site-packages/torch/lib/libhsa-runtime64.so
14. cp /opt/rocm/lib/libhsa-runtime64.so.1.14.0 venv/lib/python3.10/site-packages/triton/backends/amd/lib/libhsa-runtime64.so
15. python3.10 launch.py --precision full --no-half --listen (do not use --xformers as it will not work)
16. netsh interface portproxy set v4tov4 listenport=7860 listenaddress=127.0.0.1 connectport=7860 connectaddress=<ip address of WSL you can get it by "ifconfig">
18. http://127.0.0.1:7860

Also Training is working. I am a noob on that. I tested only to create my first embedding.

The xformers are working with Torch but A1111 is not able to correcly use them. I think something would need to be done on A1111 to addapt it for the xfomers. The issue is that AMD GPUs do not have all the support in the "ROCm/composable_kernel" (only my assumption).
