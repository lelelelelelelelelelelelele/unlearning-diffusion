## diffusion 

denoising diffusion probabilistic models”。
DDPM: https://arxiv.org/abs/2006.11239
![alt text](source/image.png)
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
   - **FID**: standard -> pre-trained CNN classification model -> representation ;   the distance between the representation of the generated images and the representation of the real images (assumption of Gaussians distribution)  
   两组distribution的距离
   limitation: need a large scale of generated images  

   - **CLIP**: An additional Image Encoder model
   CLIP score: the vectors similarity between the encoded text and encoded generated image representations
   multimodal encoder

#### decoder: 
feature: Training without knowing the correspondence between images and text 
intermediate: 
- compressed image: sample and downsample -> train
- latent representation:  auto-encoder  
    - input: H\*W\*3 latent: h\*w\*c (exceeding vision dimension)

#### generation model:
input: noised image + text  
output: intermediate  
text(additional): condition (can be ignored during inferation)
加噪过程，改为加在中间杂序上，使用auto-encoder的encoder部分
train a noise predictor
denoising: initialized by sampling normal distribution noise

### algorithm  
#### part 1 training

![alt text](source/image.png)
loss function during training:
2. xo -> clean images
4. $\epsilon$ samples from normal distribution ($\mu$ = 0,v = 1)
5. 
![alt text](source/training.jpg)
<span style="color: red;">inside</span>:  weighted sum, noising  
  the larger t is, the more proportion the noise added  
<span style="color: blue;">$\epsilon_\theta$</span> : noise predictor
input: noisy image + t(step/iteration)
output: predicted noise image  
compared with the target noise you have sampled in **step 4**  

**difference with origin steps**
noise and denoise step by step  < <u>DDPM training </u>> predicting the noise by once  
why?

#### sample
generate image
![alt text](source/sampling.jpg)
strangeness: elinimate the predicted noise and add a new one afterward (plus signal)

### theory
map the generated **distribution** to the actual world distribution
Q: to measure the similarity of the two distribution
A: maximum likelihood Estimation:(MLE)  
  $P_\theta(x)<->P_{data}(x)$  
  sample  
**all objective for image generation model**

#### KL divergence 
KL diverges: 衡量两种分布差异程度
  definition：$D_{KL}(P \| Q) = \int p(x) \log \left(\frac{p(x)}{q(x)}\right) dx$
非对称性 assymmetry
#### VAE encoder & diffusion model
q(z|x)
given the image:x, the distribution of the latent space (p(z|x))
z: distribution (major Gaussians) given the data x (x -> image to imitate)
<!-- maximize lower bound -->
maximize *lower bound of logP(x)*
VAE:
$\mathbb{E}_{q(z|x)}[\log{\frac{p(x,z)}{q(z|x)}} ]$
DDPM: z->x_0
$\mathbb{E}_{q(x_1:x_T|x)}[\log{\frac{p(x_0:x_T)}{q(x_1:x_T|x)}} ]$

## diffusers
### unet
1. Additionally, the stable diffusion U-Net is able to condition its output on text-embeddings via **cross-attention** layers.
2. short-cut connections are usually added between the downsampling ResNets of the encoder to the upsampling ResNets of the decoder
3. The cross-attention layers are added to both the encoder and decoder part of the U-Net usually between ResNet blocks.

## unlearning (erasing concepts)  
### related work  
#### concept censorship  
Prior approaches have focused on **dataset filtering [30], post-generation filtering [29], or inference guiding [38]**
- removal or guidance
post-hoc: using classifier after training
adding guidance to the inference process \*[38]
[38] Patrick Schramowski, Manuel Brack, Björn Deiseroth, and Kristian Kersting. Safe latent diffusion: Mitigating inappropriate degeneration in diffusion models. arXiv preprint arXiv:2211.05105, 2022.
sota guidance-based approach
- image cloaking
  adding adversarial perturbations
#### model edit
GAN -> diffusion model  
by a token for a new subject trained using only a handful of images  
#### unlearning
previous assumption: unintentional memorization; undesired knowledfe is identifiable on a set of training data points  
our: erase a high-level visual concept
fine tune  
### inspiration and source
set-like composition?
**energy-based models** EBM  
A and not B as the difference between log probability densities for A and B
[10], [11], [37], [38]  
score based composition  
reference: 
<!-- ![alt text](<>) -->
(source/Kimi.jpg)
### limitation
interference of others
trade off on the erasing effect and interference
tends to erase only the main elements
E: discard the car
![alt text](edited_car.png)


---