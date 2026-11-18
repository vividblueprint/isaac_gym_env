# Installation

download: [NVIDIA Isaac Gym Download](https://developer.nvidia.com/isaac-gym/download?utm_source=chatgpt.com) and extract to `~/playground/`

### Method 1: Direct Installation

```bash
cd ~/playground
git clone git@github.com:vividblueprint/isaac_gym_env.git

cd ~/playground/isaac_gym_env

uv sync

source .venv/bin/activate
```

### Method 2: Convert to UV Env

```bash
# create uv env
mkdir -p ~/playground/isaac_gym_env
cd ~/playground/isaac_gym_env

uv python install 3.8
uv venv --python 3.8
source .venv/bin/activate

uv pip install -e ../isaacgym/python

uv pip install "numpy==1.23.5"

# add uv env
uv pip freeze --python .venv/bin/python > requirements.txt
uv init --bare --python 3.8

uv add -r requirements.txt
```

# Run

```bash
cd ~/playground/isaacgym/python/examples
uv run joint_monkey.py
```

# If necessary, add it to the library search path:

```bash
#!/usr/bin/env bash

export __NV_PRIME_RENDER_OFFLOAD=1
export __VK_LAYER_NV_optimus=NVIDIA_only

exec uv run "$@"

export LD_LIBRARY_PATH="$(python -c 'import sysconfig; print(sysconfig.get_config_var("LIBDIR"))'):${LD_LIBRARY_PATH:-}"
```