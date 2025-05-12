---
title: Behind the Noise
layout: default
---

# Behind the Noise  
**Conformal Quantile Regression Drives Emergent Representations**

Our framework uses ensembles of lightweight, randomly-architected neural networks to denoise scientific images, quantify uncertainty of these predictions, and reveal semantic patterns in the all data, without any labeled data. 

---

## Abstract

Scientific imaging often demands long exposures to achieve signal clarity. We introduce a new approach that:

- **Denoises low-exposure images** using quantile regression to predict lower, median, and upper bounds.  
- **Calibrates uncertainty** via conformal prediction, giving reliable coverage guarantees.  
- **Reveals latent structure** by clustering ensemble latent outputs, producing interpretable segmentation without any supervision.

---

## Datasets

- **Synthetic data**: [phzwart/BTN_Synthetic](https://huggingface.co/datasets/phzwart/BTN_Synthetic)  
- **X-ray computed tomography of soil**: [phzwart/BTN_XCT](https://huggingface.co/datasets/phzwart/BTN_XCT)  
- **SEM-EDX of soil**: [phzwart/BTN_SEM-EDX](https://huggingface.co/datasets/phzwart/BTN_SEM-EDX)  

## Arxiv Link to Paper


