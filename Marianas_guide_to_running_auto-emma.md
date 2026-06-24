Mariana’s guide to running auto-emma

Legend

Green = success

Yellow = attempt

Step 1: Initial setup – only done once

git clone git@github.com:mitchellxh/auto-emma.git

cd auto-emma

uv venv --python 3.13

source .venv/bin/activate

uv pip install -e .

playwright install chromium

uv pip install vllm

mkdir -p /nfs/roberts/scratch/pi_epf9/mdc74/huggingface

# Also made two changes directly in the code:

Changed hf_home to hf_home: "/nfs/roberts/scratch/pi_epf9/mdc74/huggingface" in config/settings.yaml

Added module load CUDA/12.9.1 into the seup_env() in scripts/slurm/common.sh

Step 2: Normal setup – done every time we need to start the terminal

module load uv

module load CUDA/12.9.1

cd ~/auto-emma

source .venv/bin/activate

Step 3: Running the Pipeline

# Need to go to data/input/pws_names/ and find the appropriate file name for the state that you want to run

# Fresh run — Montana

bash scripts/run_pipeline.sh \

  --state MT \

  --input-file data/input/pws_names/huc12_cws_nomobile/pws-MT-20260130.xlsx

# Fresh run — Wyoming

bash scripts/run_pipeline.sh \

  --state WY \

  --input-file data/input/pws_names/huc12_cws_nomobile/pws-WY-20260130.xlsx

# Fresh run — New Mexico

bash scripts/run_pipeline.sh \

  --state NM \

  --input-file data/input/pws_names/huc12_cws_nomobile/pws-NM-20260130.xlsx

Step 4: Export data

Paste output data in shared folder

Step 5: Update clone – only when data is updated

cd /nfs/roberts/project/pi_epf9/$USER/auto-emma

git pull

module load uv

source .venv-review/bin/activate

UV_LINK_MODE=copy uv pip install -e .

Step 6: Run review

cd /nfs/roberts/project/pi_epf9/$USER/auto-emma

./review MT

cd /nfs/roberts/project/pi_epf9/$USER/auto-emma

./review WY

