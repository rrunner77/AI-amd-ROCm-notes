1. uninstall needed of any previouse ROCm drivers -> sudo amdgpu-uninstall
2. https://rocm.docs.amd.com/en/docs-7.0-rc1/preview/install/rocm.html
3. sudo apt install rocm
4. install ComfyUI
5. run venv
6. pip3.12 install --index-url https://rocm.nightlies.amd.com/v2/gfx110X-dgpu/ rocm[libraries,devel] --force-reinstall ---- https://github.com/ROCm/TheRock/blob/main/RELEASES.md#installing-pytorch-python-packages
7. run comfyUI
