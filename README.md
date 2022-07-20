# stylegan2-landscape

Code for StyleGAN2 landscape generation & Inference


## Requirements

I have tested on:

- Python 3.8.10
- CUDA 11.4

   

## 1. Landscape Generation (scripts/generate.py)

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


##  2. GAN Inversion (scripts/inference.py)

You can project input image to latent spaces.   
You can choose to use only pSp encoder, or additionally use optimization method.   

> python scripts/inference.py --image_dir IMAGE_DIR --save_dir SAVE_DIR --optimize True/False --step STEP

You **MUST** give both **--image_dir** and **--save_dir** option when running the code, otherwise it will be terminated with error message.   
   
   
### Sample scripts   
You can try GAN Inversion with sample image as follows:
> python scripts/inference.py --image_dir ./original_image.png --save_dir ./inversion_result   


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
