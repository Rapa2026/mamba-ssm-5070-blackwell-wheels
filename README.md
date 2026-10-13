# mamba-ssm-5070-blackwell-wheels
# Mamba-SSM & Causal-Conv1d Wheels for RTX 5070 / Blackwell sm_120

> **TL;DR: If you have an RTX 5070 / 5080 / 5090 and `pip install mamba-ssm` has been ruining your life for 3 days, this is for you.**

These are pre-built, working wheels for **RTX 5070 Blackwell architecture (sm_120, compute capability 12.0)**.

Built after 3 days of pain, `cp310 vs cp312` errors, `torch 2.14.1` trying to nuke my env, and `bash:!: event not found`.

**Tested working on:**
- GPU: RTX 5070 (sm_120, 12.0)
- PyTorch: 2.11.0+cu128
- Python: 3.10 (cp310)
- WSL2 + Ubuntu
- Mamba-SSM: 2.3.2.post1
- Causal-Conv1d: 1.7.0
