# Qwen Image 2.1 on Kaggle (Wan2GP)

Run Qwen Image 2.1 or Qwen Image 2.1 Turbo on a Kaggle T4 using Wan2GP. Only one GPU is used.

Heavy files go in `/tmp`. Small files stay in the working directory.

## Files

- `qwen_image_21_kaggle.ipynb` — notebook to clone, install, download weights, and launch Wan2GP

## Choose a model

Set `MODEL` in step 3 of the notebook:

| Model | `MODEL` value | Steps | CFG | Notes |
|---|---|---|---|---|
| Qwen Image 2.1 Turbo | `'turbo'` | 8 | 1 | Official Turbo, much faster |
| Qwen Image 2.1 | `'base'` | 40 | 4 | Slower, supports negative prompts |

Only the model you pick is downloaded (about 7 GB for either).

## Setup

1. Open the notebook on Kaggle with a T4 GPU and internet on.
2. Set `MODEL` to `'turbo'` or `'base'`.
3. Run the cells in order.
4. In Wan2GP, pick the model from the dropdown. And then, add the local files as a finetune (below).

### Main checkpoint

Turbo:

```
/tmp/qwen_image_21/qwen_image_21_turbo_7B_int8_convrot.safetensors
```

Base:

```
/tmp/qwen_image_21/qwen_image_21_7B_int8_convrot.safetensors
```

### Text encoder checkpoint

```
/tmp/qwen_image_21/Qwen3-VL-8B-Instruct/Qwen3-VL-8B-Instruct_int8_convrot.safetensors
```

Architecture: `qwen_image_21_7B`

Keep the default Qwen Image 2.1 VAE.

## Fix Torch Stack and NumPy

Wan2GP crashes on launch on Kaggle without this patch, so don't skip the "Fix Torch Stack and NumPy" cell in the notebook. It fixes two errors:

- PyTorch and TorchAudio built for different CUDA versions
- NumPy too new for Numba

Run it after the requirements install and before launching Wan2GP. Run it again in every fresh session.

## Settings

| Setting | Turbo | Base |
|---|---|---|
| Resolution | `1024x1024` | `1024x1024` |
| Steps | `8` | `40` |
| Guidance (CFG) | `1` | `4` |
| Scheduler | Qwen Image 2.1 Turbo (fixed sigmas) | default |
| Acceleration LoRA | none | none |
| KV Cache | Off | Off |
| Batch | `1` | `1` |

For Turbo, use Wan2GP's Turbo scheduler, not a normal FlowMatch schedule.

## Test prompt

```
A cute orange cat sitting on a wooden table beside a small cup of coffee, warm morning sunlight coming through a window, realistic photography.
```

Negative (Base only, since CFG 1 on Turbo ignores it):

```
blurry, low quality, watermark, text
```

## Credits and license

- Weights: [DeepBeepMeep/Qwen_image_2](https://huggingface.co/DeepBeepMeep/Qwen_image_2), repackaged from [Qwen/Qwen-Image-2.1](https://huggingface.co/Qwen/Qwen-Image-2.1) and [Qwen/Qwen-Image-2.1-Turbo](https://huggingface.co/Qwen/Qwen-Image-2.1-Turbo)
- App: [Wan2GP](https://github.com/deepbeepmeep/Wan2GP)
- Built with Qwen. The models are under the Qwen Research License (non-commercial research use). Check it before using outputs commercially.
