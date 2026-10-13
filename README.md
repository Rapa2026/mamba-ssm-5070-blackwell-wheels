
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
- Built with the help of Meta AI
  
http://torch.Size(212864)
MAMBA FORWARD OK ON 5070[2][128][64]

The Wheels (in Releases)

- `causal_conv1d-1.7.0-cp310-cp310-linux_x86_64.whl` (169 MB)
- `mamba_ssm-2.3.2.post1-cp310-cp310-linux_x86_64.whl` (277 MB)

How to use

```bash
1. Make the right env - MUST be python 3.10
conda create -n mamba5070 python=3.10 -y
conda activate mamba5070

2. Install torch cu128 FIRST - don't let mamba overwrite it
pip install torch==2.11.0 --index-url https://download.pytorch.org/whl/cu128

3. Install these wheels with --no-deps so it doesn't install torch 2.14.1
pip install causal_conv1d-*.whl --no-deps --no-build-isolation --force-reinstall
pip install mamba_ssm-*.whl --no-deps --no-build-isolation --force-reinstall

4. Install the tiny deps it actually needs
pip install einops huggingface_hub transformers

5. Victory test
python -c "import mamba_ssm; import causal_conv1d; print('BOTH OK'); import torch; print(torch.__version__, torch.cuda.get_device_capability())"
Should print: BOTH OK / 2.11.0+cu128 (12, 0)

python -c "import torch; from mamba_ssm.modules.mamba2 import Mamba2; m=Mamba2(d_model=64).cuda(); x=torch.randn(2,128,64).cuda(); print(m(x).shape)"
Should print: torch.Size([2, 128, 64])
Why --no-deps?

Because `mamba-ssm 2.3.2` declares `torch`, `triton`, `tvm-ffi`, `quack-kernels`, `tilelang` as dependencies. If you `pip install` normally, pip will downgrade/upgrade your torch to `2.14.1` and break Blackwell support. We install the CUDA kernels only.

Disclaimer

These wheels were built in Docker (`pytorch/pytorch:2.5.1-cuda12.4-cudnn9-devel`) then `docker cp`'d out. Original code is from state-spaces/mamba and Dao-AILab/causal-conv1d. I don't own the code, just the pain of compiling it for sm_120.

Credits

I was the human slave who typed all the commands. My AI overlord told me what to do. Honestly I still don't fully know what an "attention thing" is but it works now.

If this saved you 3 days, give it a star.

- Built in Manchester, UK, 13/10/2026
