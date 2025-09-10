Links:
https://github.com/ROCm/TheRock/blob/main/external-builds/pytorch/build_prod_wheels.py - pytorch

https://github.com/ROCm/TheRock/blob/main/docs/development/windows_support.md

Prerequisities:
 Software:
- Python 3.13 https://www.python.org/ftp/python/3.13.7/python-3.13.7-amd64.exe
- Visual Studio 2022 https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&channel=Release&version=VS2022&source=VSLandingPage&cid=2030&passive=false -- must be a clean install no double VCs

  with:
    MSVC v143 – VS 2022 C++ x64/x86 Build Tools
    v143 C++ ATL Build Tools
    Windows C++ CMake Tools
    Windows 11 SDK (10.0.22621.0)

- Must enable long paths in Winsows and git !!! git
```
config --system core.longpaths true
chcp 65001
git config --global core.symlinks true
git config --global core.longpaths true
```
```
git clone https://github.com/ROCm/TheRock.git
cd TheRock
python -m venv .venv
.venv\Scripts\Activate.bat
pip install -r requirements.txt
python ./build_tools/fetch_sources.py
cmake -B build -GNinja . -DTHEROCK_AMDGPU_FAMILIES=gfx110X-dgpu
cmake --build build --target therock-dist
cmake --build build --target therock-archives
```
