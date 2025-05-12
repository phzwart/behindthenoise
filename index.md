---
title: Behind the Noise
layout: default
---

# Behind the Noise  
**Conformal Quantile Regression Drives Emergent Representations**

Our framework uses ensembles of lightweight, randomly-architected neural networks to denoise scientific images, quantify uncertainty of these predictions, and reveal semantic patterns in the data, without needing to provide human annotated labels. 

---

## Abstract

Scientific imaging often demands long exposures to achieve signal clarity. We introduce a new approach that:

- **Denoises low-exposure images** using quantile regression to predict lower, median, and upper bounds.  
- **Calibrates uncertainty** via conformal prediction, giving reliable coverage guarantees.  
- **Reveals latent structure** by clustering ensemble latent outputs, producing interpretable segmentation without any supervision.

---

## Outline

The proposed workflow uses small networks constructed from a stochastic network generator. These networks have a low number of parameters, are not super deep, and explore scale space via dilated convolutions. Fine tuning the networks is straightforward, and typically only requieres tuning the depth - more finetuning can be done to manage memory requirements or tuning the complexity. 

![Random networks](assets/images/Suplementary_Figure1.png)  
*Figure 1: Random networks and their performance on synthetic data.*

Note that the networks we generate have two main parts: a convolutional neural network that serves as an encoder yielding pixel-level latent vec tors. These latent vectors are pushed into decoders that model lower, median and upper quantiles, Figure 1-A. The performance of these networks as a function of hyper parameters are shown in Figure 1-B. 

Once we have determined a set of hyper parameters we like, we can generate a set of random networks. The ensemble of networks can be used to improve our quantile estimates by simple averaging the outputs:

![ Ensembling networks](assets/images/Figure1.png)
*Figure 2: Ensembles improve the estimates of the predicted quantiles. Results are obtained by averaging over 20 different ensembles of random networks per trial.*

While we-  that is, the minimizer during training - do our best to get decent quantile estimates, they *always* need to be caliberated to ensure that the stated coverage (say 90%) is valid on unseen data. The way this is done is via [conformalized quantile regression](https://arxiv.org/abs/1905.03222).

Below an sample of the results is shown, including line cuts with the associated prediction intervals

![Enselmbing results](assets/images/Suplementary_Figure2.png)
*Figure 3: Denoising synthetic data with assymetric, heteroskedastic noise.*

We apply these techniques on SEM-EDX data
![SEM-EDX example](assets/images/Suplementary_Figure3.png)
*Figure 4: SEM-EDX training.*

If we now run this on unsee data, we get decent 
![SEM-EDX example](assets/images/Figure2.png)
*Figure 5: SEM-EDX testing.*



## Datasets

- **Synthetic data**: [phzwart/BTN_Synthetic](https://huggingface.co/datasets/phzwart/BTN_Synthetic)  
- **X-ray computed tomography of soil**: [phzwart/BTN_XCT](https://huggingface.co/datasets/phzwart/BTN_XCT)  
- **SEM-EDX of soil**: [phzwart/BTN_SEM-EDX](https://huggingface.co/datasets/phzwart/BTN_SEM-EDX)  

## Code
The research carried out in the Behind The Noise paspert is based on out DLSIA libraries.
- [DLSIA (Deep Learning for Scientific Imaging & Automation)](https://github.com/phzwart/dlsia)

Training was facilitated by our sliding tensor data chopper qlty: 
- [qlty (Tensor chunking & stitching for PyTorch)](https://github.com/phzwatr/qlty)  


## Arxiv Link to Paper


