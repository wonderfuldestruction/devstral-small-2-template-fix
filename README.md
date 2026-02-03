# Devstral Small 2 - Chat Template Fix

## Issue

The implemented chat templates break agentic tool usage in environments like Kilocode (and forks alike) and Openclaw where jinja breaks apart during unsupported role usage, triggering an exception error 500.

**Error Trigger Examples**
- Kilocode context compaction
- Kilocode subtask completion to Orchestrator
- Kilocode randomly breaking mid-session
- Openclaw unusable in any shape

**Tested Stack**
```
llama.cpp b7907
Devstral Small 2 Unsloth Q8_0 or LM Studio Q8_0
```

## The Fix

The patch was implemented by adding an exception for unsupported roles by modifying Unsloth's chat template used in their Devstral Small 2 HF repo (https://huggingface.co/unsloth/Devstral-Small-2-24B-Instruct-2512-GGUF).

### Guide for Dummies

- Download jinja file from this repo or, create a jinja file (e.g. `devstral-fix.jinja`) and paste the chat template inside.
- Use `--chat-template-file` flag in llama.cpp to point to new jinja file (e.g. `--chat-template-file /path/devstral-fix.jinja`)
- Disable `--jinja` flag as this will override the new template.

_Credits belongs to Unsloth and Mistral respectively._
