--------------------
Install drivers
--------------------
wget https://repo.radeon.com/amdgpu-install/7.2/ubuntu/noble/amdgpu-install_7.2.70200-1_all.deb
sudo apt install ./amdgpu-install_7.2.70200-1_all.deb
sudo apt update
sudo apt install python3-setuptools python3-wheel
sudo usermod -a -G render,video $LOGNAME # Add the current user to the render and video groups
sudo apt install rocm

--------------------
ComfyUi
--------------------
git clone https://github.com/comfyanonymous/ComfyUI.git ComfyUI-rocm72

--------------------
create venv
--------------------
cd ComfyUI-rocm72
python3.12 -m venv .venv
source .venv/bin/activate

--------------------
Install torch
--------------------
python3.12 -m pip install --upgrade pip wheel
pip3.12 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/rocm7.2/


git clone https://github.com/ROCm/flash-attention.git
cd flash-attention
git checkout main_perf
pip install packaging
FLASH_ATTENTION_TRITON_AMD_ENABLE="TRUE" python setup.py install
pip install sageattention

--------------------
Flash Attention File Replacement
--------------------
Replace the following file in myvenv/lib/python3.12/site-packages/flash_attn/utils/:

[distributed.py](https://github.com/patientx/ComfyUI-Zluda/tree/master/comfy/customzluda/fa/distributed.py)

--------------------
SageAttention File Replacements
--------------------
Replace the following files in myvenv/lib/python3.12/site-packages/sageattention/:

  [attn_qk_int8_per_block.py](https://github.com/patientx/ComfyUI-Zluda/blob/master/comfy/customzluda/sa/attn_qk_int8_per_block.py)
  
  [attn_qk_int8_per_block_causal.py](https://github.com/patientx/ComfyUI-Zluda/blob/master/comfy/customzluda/sa/attn_qk_int8_per_block_causal.py)
  
  [quant_per_block.py](https://github.com/patientx/ComfyUI-Zluda/blob/master/comfy/customzluda/sa/quant_per_block.py)
