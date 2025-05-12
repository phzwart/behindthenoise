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
*Figure: Random networks and their performance on synthetic data.*

Once 

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


