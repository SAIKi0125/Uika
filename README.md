# UIKA on Extreme Parkour

This repository is a customized version of `extreme-parkour` for the UIKA quadruped.

## What Is Included

- UIKA robot asset and URDF integration
- UIKA task config: `legged_gym/legged_gym/envs/uika/uika_parkour_config.py`
- Flat-ground training script: `legged_gym/legged_gym/scripts/train_uika_flat.py`
- Flat-ground play script: `legged_gym/legged_gym/scripts/play_uika_flat.py`
- URDF and contact diagnostics:
  - `legged_gym/legged_gym/scripts/check_uika_urdf.py`
  - `legged_gym/legged_gym/scripts/play_test.py`
  - `legged_gym/legged_gym/scripts/urdf_play_test.py`

## Environment Setup

Use the exported conda environment:

```bash
conda env create -f requirements/conda/parkour.yml
conda activate parkour
```

Minimal pip requirements are also available in:

```bash
requirements/parkour-requirements.txt
```

## Training

### 1. Flat-ground pretraining (recommended first step)

```bash
cd legged_gym/legged_gym/scripts
python train_uika_flat.py --task uika --proj_name parkour_flat --exptid uika-flat-001 --num_envs 2048
```

### 2. Continue training on normal terrain

```bash
cd legged_gym/legged_gym/scripts
python train.py --task uika --proj_name parkour_flat --exptid uika-rough-001 --resume --resumeid uika-flat-001 --num_envs 2048
```

## Playback / Evaluation

### Flat-ground policy playback

```bash
cd legged_gym/legged_gym/scripts
python play_uika_flat.py --task uika --proj_name parkour_flat --exptid uika-flat-001 --checkpoint 300
```

### URDF standing/contact check

```bash
cd legged_gym/legged_gym/scripts
python check_uika_urdf.py --task uika --headless --num_envs 1
```

## Useful Notes

- Use `--proj_name` and `--exptid` consistently between train/play, otherwise checkpoint loading will fail.
- If `play.py` or `train.py` cannot find models, verify the path under `legged_gym/logs/<proj_name>/<exptid>/`.
- For GitHub remote:
  - `origin`: your own repo
  - `upstream`: original `extreme-parkour` repo
