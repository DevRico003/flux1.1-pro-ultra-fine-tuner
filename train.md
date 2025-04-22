# FLUX 1.1 Pro Ultra Fine-Tuner

Train a LoRA (Low-Rank Adaptation) for FLUX 1.1 Pro Ultra.

## Basic Training Example

Here's a basic example of how to train a LoRA:

```python
import replicate

training = replicate.trainings.create(
    version="devrico003/flux-pro-ultra-lora-trainer",
    input={
        "input_images": "https://example.com/path-to-your-images.zip",
        "trigger_word": "YOUR_TRIGGER_WORD",
        "steps": 2000
    },
    destination="devrico003/your-flux-lora"
)

print(f"Training URL: https://replicate.com/p/{training.id}")
```

## Training Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `input_images` | A zip file containing the images that will be used for training. We recommend a minimum of 10 images. | *Required* |
| `trigger_word` | The trigger word to associate with your concept. | `"TOK"` |
| `autocaption` | Automatically caption images using Llava v1.5 13B. | `true` |
| `autocaption_prefix` | Text to appear at the beginning of all generated captions. | *(Optional)* |
| `autocaption_suffix` | Text to appear at the end of all generated captions. | *(Optional)* |
| `steps` | Number of training steps. | `1000` |
| `learning_rate` | Learning rate for training. | `4e-4` |
| `batch_size` | Batch size for training. | `1` |
| `resolution` | Image resolutions for training. | `"512,768,1024"` |
| `lora_rank` | Higher ranks capture more complex features. | `16` |
| `caption_dropout_rate` | Controls how often captions are ignored during training. | `0.05` |
| `optimizer` | Optimizer to use for training. | `"adamw8bit"` |
| `cache_latents_to_disk` | Use for lots of input images to avoid memory errors. | `false` |
| `gradient_checkpointing` | Trade training speed for memory efficiency. | `false` |
| `hf_repo_id` | Hugging Face repository ID to upload the trained LoRA. | *(Optional)* |
| `hf_token` | Hugging Face token for uploading the LoRA. | *(Optional)* |
| `wandb_api_key` | Weights and Biases API key for logging. | *(Optional)* |
| `wandb_project` | Weights and Biases project name. | `"flux_train_replicate"` |

## Advanced Example

Here's an advanced example with more customization:

```python
import replicate

training = replicate.trainings.create(
    version="devrico003/flux-pro-ultra-lora-trainer",
    input={
        "input_images": "https://example.com/your-images.zip",
        "trigger_word": "custom_style",
        "steps": 2000,
        "learning_rate": 0.0004,
        "lora_rank": 16,
        "batch_size": 1,
        "resolution": "512,768,1024",
        "optimizer": "adamw8bit",
        "autocaption": True,
        "caption_dropout_rate": 0.05,
        "gradient_checkpointing": False,
        "hf_repo_id": "your-username/your-model-name",
        "hf_token": "hf_..."
    },
    destination="your-username/your-flux-lora"
)

print(f"Training URL: https://replicate.com/p/{training.id}")
```