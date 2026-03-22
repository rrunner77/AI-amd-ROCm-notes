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
