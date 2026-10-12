## How to run claude-cli with ollama backend

```
export ANTHROPIC_BASE_URL=http://localhost:11434/v1
export CLAUDE_CODE_MAX_OUTPUT_TOKENS=128000
export PATH="$HOME/.local/bin:$PATH"

ollama launch claude
```

- Best model was the Qwen 3.8 27B

Change the ollama setup for the max context is required !!! the context need to be 256K minimum
