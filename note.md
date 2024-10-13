### diffusion 

denoising diffusion probabilistic models”。
DDPM: https://arxiv.org/abs/2006.11239
![alt text](image.png)
Input: noised image + iteration  
model
output: noise predicted -> denoising

### stable diffusion  
1. text encoder to vector  
2. generation model (diffusion) Denoising U-Net  
3. decoder to final version in pixel space
parallel training   
mid journey: during training process, illustrates the results encoded from the denoising images

#### text encoder:
1. gpt coding/ BIRT
1. criteria: CLIP score/ FID-10k  
   - **FID**: standard -> pre-trained CNN classification model -> representation ；   the distance between the representation of the generated images and the representation of the real images (assumption of Gaussians distribution)  
   两组distribution的距离
   limitation: need a large scale of generated images  

   - **CLIP**: An additional Image Encoder model
   CLIP score: the vectors similarity between the encoded text and encoded generated image representations
 
#### decoder: 
feature: Training without knowing the correspondence between images and text 
intermediate: 
- compressed image: sample and downsample -> train
- latent representation:  auto-encoder  ??
    - input: H\*W\*3 latent: h\*w\*c (exceeding vision dimension)

#### generation model:
input: noised image + text  
output: intermediate  
加噪过程，改为加在中间杂序上，使用auto-encoder的encoder部分
train a noise predictor
denoising: initialized by sampling normal distribution noise
<!-- 
#### VAE & diffusion model -->
### algorithm  
#### part 1 training

![alt text](source/image.png)
loss function during training:
2. xo -> clean images
4. $\epsilon$ samples from normal distribution ($\mu$ = 0,v = 1)
5. 
![alt text](source/training.jpg)
<span style="color: red;">inside</span>: weighted sum, noising  
  the larger t is, the more proportion the noise added
<span style="color: blue;">$\epsilon_\theta$</span> : noise predictor
compared with the target noise you have sampled in **step 4**



---