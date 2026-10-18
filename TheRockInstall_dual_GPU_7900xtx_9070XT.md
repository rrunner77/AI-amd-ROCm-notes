# Install the pip for 7900XTX and 9070XT:

```
pip install --index-url https://nightly.repo.amd.com/rocm/whl-next/ \
    "rocm[libraries,device-gfx1100,device-gfx1201]"

pip install --index-url https://nightly.repo.amd.com/rocm/whl-next/ \
    "torch[device-gfx1100,device-gfx1201]" \
    "torchvision[device-gfx1100,device-gfx1201]" \
    torchaudio
````

#Verify if the cards work:
```
import torch

print(torch.cuda.is_available())
# True
print(torch.cuda.get_device_name(0))
print(torch.cuda.get_device_name(1))
```
