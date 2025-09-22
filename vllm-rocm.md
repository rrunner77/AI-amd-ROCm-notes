How to install VLLM

install docker:
```
docker run -it \
   --network=host \
   --group-add=video \
   --ipc=host \
   --cap-add=SYS_PTRACE \
   --security-opt seccomp=unconfined \
   --device /dev/kfd \
   --device /dev/dri \
   -v /ai/vllm:/app/model \
   vllm-rocm \
   bash
```
Parameters which work with 7900XTX (most problematic is the caches which increase the VRAM usage):
- max_num_seqs => It specifies the maximum number of sequences (e.g., prompts, input texts, or batches of tokens) that the model can process simultaneously. - personal use 16-32 on a consumer GPU
- max_seq_len_to_capture => This parameter ensures that the model only processes sequences up to a certain length, balancing speed  - on consumer GPU: 20–50
- max_num_batched_tokens => It specifies the maximum total number of tokens (across all sequences in a batch) that the model can process at once. - personal use -> 1024–2048 on a consumer GPU
- max_model_len => should be set to model len -> if you have VRAM :)
```
model=Qwen/Qwen3-8B
tp=1
dtype=auto
kv_cache_dtype=auto
max_num_seqs=512  
max_seq_len_to_capture=32768
max_num_batched_tokens=32768
max_model_len=2048
```
Run vllm inside the docker
```
vllm serve $model   \
-tp $tp     \
--dtype $dtype     \
--kv-cache-dtype $kv_cache_dtype     \
--max-num-seqs $max_num_seqs     \
--max-seq-len-to-capture $max_seq_len_to_capture     \
--max-num-batched-tokens $max_num_batched_tokens     \
--max-model-len $max_model_len
```
