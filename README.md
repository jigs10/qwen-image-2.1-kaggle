# Qwen Image 2.1 on Kaggle (Wan2GP)

Run Qwen Image 2.1 on a Kaggle T4 using Wan2GP. Only one GPU is used.

Heavy files go in `/tmp`. Small files stay in the working directory.

## Files

- `qwen_image_21_kaggle.ipynb` — notebook to clone, install, download weights, and launch Wan2GP

## Setup

1. Open the notebook on Kaggle with a T4 GPU and internet on.
2. Run the cells in order.
3. In Wan2GP, add the local files as a finetune.

### Main checkpoint

```
/tmp/qwen_image_21/qwen_image_21_7B_int8_convrot.safetensors
```

### Text encoder checkpoint

```
/tmp/qwen_image_21/Qwen3-VL-8B-Instruct/Qwen3-VL-8B-Instruct_int8_convrot.safetensors
```

Architecture: `qwen_image_21_7B`

Keep the default Qwen Image 2.1 VAE.

## Settings

- Resolution: `1024x1024`
- Steps: `40`
- Guidance: `4`
- KV Cache: Off
- Batch: `1`

## Test prompt

```
A cute orange cat sitting on a wooden table beside a small cup of coffee, warm morning sunlight coming through a window, realistic photography.
```

Negative:

```
blurry, low quality, watermark, text
```
