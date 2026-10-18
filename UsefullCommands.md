See the kv_cache and split to CPU/GPU
```
journalctl -u ollama --since "22:17" --no-pager | grep -iE "model buffer|offloaded|KV buffer|inference compute"
```
See the model info for the ctx
```
journalctl -u ollama --since "23:00" | grep -Ei "n_ctx|n_seq|parallel|type_k|type_v"
```
which cards are present in system
```
rocminfo | grep 'Marketing Name'
```
Power consumption
```
watch -n 0.5 'sensors | grep -iE "amdgpu|PPT|power"'
```
