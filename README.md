# stylegan2-landscape-cinemagraph

Code for StyleGAN2 landscape cinemagraph generation.   
You can also try random landscape image generation & Image GAN Inversion.


## Requirements

I have tested on:

- Python 3.8.10
- CUDA 11.4


## 1. Cinemagraph Generation (scripts/cinemagraph.py)

You can generate landscape cinemagraph from **image** and **optical flow** input:

> python scripts/cinemagraph.py --image_dir IMAGE_DIR --flow_dir FLOW_DIR --save_dir SAVE_DIR --n_frames N_FRAMES --n_loops N_LOOPS --optimize True/False --step STEP --style_image_dir STYLE_DIR

You **MUST** give **-image_dir**, **--flow_dir**, and **--save_dir** option when running the code, otherwise it will be terminated with error message.   

### Sample Script
You can try cinemagraph generation with sample image and optical flow as follows:   
> python scripts/cinemagraph.py --image_dir ./original_image.png --flow_dir ./optical_flow.pth --save_dir ./loop_result


### Arguments

Arguments are defined in **utils/cinemagraph_utils.py**, at **set_args()** function.

- **--image_dir**:         Directory of input image.
- **--flow_dir**:          Directory of optical flow.
- **--style_image_dir**:   Directory of style image. You can apply style of style image onto the original image.
- **--n_frames**:          Number of frames for one cycle of looping animation.
- **--n_loops**:           Number of loops to be repeated.
- **--loop**:              Generate cinemagraph = True, else = False. If False, only GAN Inversion would be performed.
- **--pSp_dir**:           Checkpoint directory of pretrained pSp encoder model.
- **--stylegan2_dir**:     Checkpoint directory of pretrained StyleGAN2 model.
- **--optmize**:           Whether to use additional optimization method or not. (Default: True)
- **--step**:              Optimization steps. Recommend the value between 2000 and 3000 for perfect reconstruction.
- **--initial_lr**:        Initial learning rate for optimization process. (Default: 0.1)
- **--lpips**:             Coefficient of LPIPS loss when calculating total loss. (Default: 0.2)
- **--mse**:               Coefficient of MSE loss when calculating total loss. (Default: 1.0)
- **--channel_multiplier**: Channel multiplier of StyleGAN2 generator. Recommend not to change.      


##  2. GAN Inversion (scripts/inference.py)

You can project input image to latent spaces.   
You can choose to use only pSp encoder, or additionally use optimization method.   

> python scripts/inference.py --image_dir IMAGE_DIR --save_dir SAVE_DIR --optimize True/False --step STEP

You **MUST** give both **--image_dir** and **--save_dir** option when running the code, otherwise it will be terminated with error message.   
You can also do it with **scripts/cinemagraph.py**, with **--loop False** option.
   
   
### Sample Script   
You can try GAN Inversion with sample image as follows:
> python scripts/inference.py --image_dir ./original_image.png --save_dir ./inversion_result   
   
or   
   
> python scripts/cinemagraph.py --image_dir ./original_image.png --save_dir ./inversion_result --loop False

### Arguments

Arguments are defined in **utils/inference_utils.py**, at **set_args()** function.

- **--pSp_dir**:           Checkpoint directory of pretrained pSp encoder model.
- **--stylegan2_dir**:     Checkpoint directory of pretrained StyleGAN2 model.
- **--image_dir**:         Directory of input image.
- **--save_dir**:          Save directory of original image, reconstructed image, w+ code *(and optimized feature map when --optimize True)*.
- **--optmize**:           Whether to use additional optimization method or not. (Default: True)
- **--step**:              Optimization steps. Recommend the value between 2000 and 3000 for perfect reconstruction.
- **--initial_lr**:        Initial learning rate for optimization process. (Default: 0.1)
- **--lpips**:             Coefficient of LPIPS loss when calculating total loss. (Default: 0.2)
- **--mse**:               Coefficient of MSE loss when calculating total loss. (Default: 1.0)
- **--channel_multiplier**: Channel multiplier of StyleGAN2 generator. Recommend not to change.

   

## 3. Landscape Generation (scripts/generate.py)

You can generate random landscape image samples with pretrained StyleGAN2 model:   

> python scripts/generate.py --save_dir SAVE_DIR --sample N_SAMPLE --pics N_PICS --style_dim STYLE_DIM

You **MUST** give **--save_dir** option when running the code, otherwise it will be terminated with error message.   

   
### Arguments

Arguments are defined in **utils/generate_utils.py**, at **set_args()** function.

- **--stylegan2_dir**:     Checkpoint directory of pretrained StyleGAN2 model.
- **--save_dir**:          Save directory for generated images.
- **--sample**:            Number of samples to be generated for each image.
- **--pics**:              Number of images to be generated.
- **--style_dim**:         Dimension of style vector. (eg) if --style_dim 18, then style vector size would be [1, 18, 512])
- **--channel_multiplier**: Channel multiplier of the generator. Recommend not to change.
- **--truncation**:        Truncation ratio.
- **--truncation_mean**:   Number of vectors to calculate mean for truncation.



