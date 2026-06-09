# Flux Model Plugin for dashAI

This plugin integrates Black Forest Labs' FLUX.1 text-to-image models into the dashAI platform using the Hugging Face `diffusers` backend. It enables high-quality image generation from text prompts and supports private access using a Hugging Face API token.

## Included Models

### 1. FLUX.1 dev
Guidance-distilled model for high-quality generation, based on [`black-forest-labs/FLUX.1-dev`](https://huggingface.co/black-forest-labs/FLUX.1-dev).

### 2. FLUX.1 schnell
Timestep-distilled model optimized for fast, few-step generation, based on [`black-forest-labs/FLUX.1-schnell`](https://huggingface.co/black-forest-labs/FLUX.1-schnell).

Both models are rectified-flow transformers, designed for high-quality image generation and compatible with CPU or GPU inference through `diffusers`.

## About Flux

FLUX.1 is a family of state-of-the-art text-to-image models from Black Forest Labs, built on a rectified-flow transformer architecture.

Key features of FLUX.1 models:

- Rectified-flow transformer: strong prompt adherence and image quality
- Two variants: `dev` for quality, `schnell` for speed
- Text-conditioned: images are guided by natural language prompts
- Negative prompting: steer the model away from unwanted elements
- Open weights with access control via Hugging Face

FLUX.1 is designed for deployment on desktops and cloud infrastructure, making advanced image generation more accessible.

## Features

- Image generation from text prompts
- Both `dev` and `schnell` variants selectable at runtime
- Reproducible generation via fixed random seeds
- Automatic login to Hugging Face to access gated models
- Configurable generation parameters:
  - `negative_prompt`: elements to avoid in the image
  - `num_inference_steps`: number of denoising steps
  - `guidance_scale`: how strongly the model follows the prompt
  - `width` / `height`: output image dimensions
  - `num_images_per_prompt`: number of images per prompt
  - `device`: detected GPU (e.g. `"GPU 0: NVIDIA RTX 3090 - Compute Capability 8.6"`) or `"CPU"`

## Model Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `model_name` | FLUX.1 model ID from Hugging Face | `"black-forest-labs/FLUX.1-dev"` |
| `huggingface_key` | Hugging Face API token to access restricted models | Required |
| `negative_prompt` | Text prompt for elements to avoid in the image | `""` (optional) |
| `num_inference_steps` | Number of denoising steps (higher = better quality, slower) | 15 |
| `guidance_scale` | How strongly the model follows the prompt | 3.5 |
| `seed` | Random seed for reproducibility (negative = random) | -1 |
| `width` | Width of the generated image (multiple of 8) | 512 |
| `height` | Height of the generated image (multiple of 8) | 512 |
| `num_images_per_prompt` | Number of images to generate per prompt | 1 |
| `device` | Inference device — a detected GPU by name (e.g. `"GPU 0: NVIDIA RTX 3090 - Compute Capability 8.6"`) or `"CPU"` | First detected GPU if available, else `"CPU"` |

## Requirements

- `diffusers`
- `torch`
- Valid Hugging Face Access Token
- Model files from Hugging Face:
  - [`black-forest-labs/FLUX.1-dev`](https://huggingface.co/black-forest-labs/FLUX.1-dev)
  - [`black-forest-labs/FLUX.1-schnell`](https://huggingface.co/black-forest-labs/FLUX.1-schnell)

**Access Notice:** You must accept the model terms on Hugging Face and use a valid Hugging Face token.
This repository is publicly accessible, but gated. You need to agree to share your contact information to access the model files.

## Notes

This plugin uses the Hugging Face `diffusers` pipeline for text-to-image generation.

The models are pretrained for inference and are not designed for fine-tuning through this plugin.
Image dimensions must be multiples of 8.
