Prerequisities:
 Software:
- Python 3.13 https://www.python.org/ftp/python/3.13.7/python-3.13.7-amd64.exe
- Visual Studio 2022 https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&channel=Release&version=VS2022&source=VSLandingPage&cid=2030&passive=false
  with:
    MSVC v143 – VS 2022 C++ x64/x86 Build Tools
    v143 C++ ATL Build Tools
    Windows C++ CMake Tools
    Windows 11 SDK (10.0.22621.0)

- Must enable long paths in Winsows !!!
1. git clone https://github.com/ROCm/TheRock.git
2. cd TheRock
3. python -m venv .venv
4. .venv\Scripts\Activate.bat
5. pip install -r requirements.txt
6. python ./build_tools/fetch_sources.py
7. cmake -B build -GNinja . -DTHEROCK_AMDGPU_FAMILIES=gfx110X-dgpu
8. cmake --build build
