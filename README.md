# stylegan2-landscape

Code for StyleGAN2 landscape generation & Inference


## Requirements

I have tested on:

- Python 3.8.10
- CUDA 11.4

   

## 1. Landscape Generation

You can generate random landscape image samples with pretrained StyleGAN2 model:   

> python scripts/generate.py --save_dir SAVE_DIR --sample N_SAMPLE --pics N_PICS --style_dim STYLE_DIM

You **MUST** give **--save_dir** option when running the code, otherwise it will be terminated with error message.   

   
### Arguments

Arguments are defined in utils/generate_utils.py, at set_args() function.

- --stylegan2_dir: Checkpoint directory of pretrained StyleGAN2 model.
