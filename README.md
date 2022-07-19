# stylegan2-landscape

### Requirements
I have tested on:
+ python 3.8.10
+ CUDA 11.4

----------
### 1. Landscape Generation (scripts/generate.py)
You can generate random landscape image samples with pretrained StyleGAN2 model:
> python scripts/generate.py --save_dir SAVE_DIR --stylegan2_dir STYLEGAN_DIR --sample N_SAMPLE --pics N_PICS --style_dim STYLE_DIM --channel_multiplier CHANNEL_MULTIPLIER --truncation TRUNCATION --truncation_mean TRUNCATION_MEAN


You **MUST** give --save_dir when running the code, otherwise it will be terminated with error message.


_____________
### 2. GAN Inversion (scripts/inference.py)
You can convert an input image into w+ and feature map:
> python scripts/inference.py --image_dir IMAGE_DIR --save_dir SAVE_DIR --pSp_dir PSP_DIR --stylegan2_dir STYLEGAN_DIR --channel_multiplier CHANNEL_MULTIPLIER --optimize True/False --step STEP --lpips LPIPS --mse MSE

You **MUST** given --save_dir and --image_dir when running the code, otherwise it will be terminated with error message.   
   
You can choose to use optimization process for better reconstruction result with *--optimize True* option, else you can only
get w+ representation with *--optimize False* option.   
