--------------------
Install drivers
--------------------
```
wget https://repo.radeon.com/amdgpu-install/7.2/ubuntu/noble/amdgpu-install_7.2.70200-1_all.deb
sudo apt install ./amdgpu-install_7.2.70200-1_all.deb
sudo apt update
sudo apt install python3-setuptools python3-wheel
sudo usermod -a -G render,video $LOGNAME # Add the current user to the render and video groups
sudo apt install rocm
```

--------------------
ComfyUi
--------------------
```
git clone https://github.com/comfyanonymous/ComfyUI.git ComfyUI-rocm72\
```

--------------------
create venv
--------------------
```
cd ComfyUI-rocm72
python3.12 -m venv .venv
source .venv/bin/activate\
```

--------------------
Install torch
--------------------
```
python3.12 -m pip install --upgrade pip wheel
pip3.12 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/nightly/rocm7.2/
```


```
git clone https://github.com/ROCm/flash-attention.git
cd flash-attention
git checkout main_perf
pip install packaging
FLASH_ATTENTION_TRITON_AMD_ENABLE="TRUE" python setup.py install
pip install sageattention
```

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
--------------------
Run with shell script
--------------------
```
#!/bin/bash
export PYTHONPATH=/opt/rocm/lib:$PYTHONPATH
#export MIGRAPHX_MLIR_USE_SPECIFIC_OPS="attention"
export PYTORCH_TUNABLEOP_ENABLED=1
export TORCH_ROCM_AOTRITON_ENABLE_EXPERIMENTAL=1
export MIOPEN_FIND_MODE=2
export PYTORCH_HIP_ALLOC_CONF=expandable_segments:True

export FLASH_ATTENTION_TRITON_AMD_ENABLE="TRUE"
export MIOPEN_LOG_LEVEL=3
export PYTORCH_TUNABLEOP_ENABLED=1

cd ComfyUI-rocm72
source .venv/bin/activate
python3.12 main.py \
    --reserve-vram 0.1 \
    --preview-method auto \
    --use-sage-attention \
    --bf16-vae \
    --disable-xformers \
    --listen
```
