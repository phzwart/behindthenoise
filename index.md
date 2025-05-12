\---
title: Behind the Noise
layout: default
---

# Behind the Noise  
**Conformal Quantile Regression Drives Emergent Representations**

Our approach uses ensembles of small, randomly-generated neural networks to denoise scientific images, quantify prediction uncertainty, and reveal hidden structures in the data—all without any hand-labeled annotations.

---

## Abstract

Scientific imaging often requires long exposures to capture clear signals. We propose a new method that:

- **Denoises low-exposure images** by predicting lower, median, and upper quantiles.  
- **Calibrates uncertainty** with conformalized quantile regression for reliable coverage guarantees.  
- **Discovers latent structure** by clustering ensemble outputs into interpretable segments without supervision.

---

## Workflow

We generate compact networks using a stochastic architecture generator. These nets are shallow, parameter-efficient, and use dilated convolutions to cover multiple scales. Typically, only the depth needs tuning, with further refinements to balance memory and complexity.

![Random networks](assets/images/Suplementary_Figure1.png)  
*Figure 1: Examples of random networks and their performance on synthetic data.*

Each network has two parts: a convolutional encoder that maps each pixel to a latent vector (Figure 1-A) and three decoder heads that predict lower, median, and upper quantiles. Figure 1-B shows how performance varies across hyperparameters.

After selecting preferred hyperparameters, we build an ensemble and average their quantile outputs:

![Ensembling networks](assets/images/Figure1.png)  
*Figure 2: Averaged quantile estimates from 20 random-network ensembles.*

Even with careful training, predicted intervals must be calibrated to achieve nominal coverage (e.g., 90%). We use [conformalized quantile regression](https://arxiv.org/abs/1905.03222) for this step.

Below is a sample of denoising results with asymmetric, heteroskedastic noise:

![Ensembling results](assets/images/Suplementary_Figure2.png)  
*Figure 3: Denoising synthetic data with asymmetric, heteroskedastic noise.*

---

## Applications

### SEM-EDX

We apply our method to three-channel SEM-EDX maps:

![SEM-EDX example](assets/images/Suplementary_Figure3.png)  
*Figure 4: SEM-EDX training data.*

On unseen samples, denoising yields clear material contrasts:

![SEM-EDX example](assets/images/Figure2.png)  
*Figure 5: Denoising SEM-EDX results on unseen data.*

Clustering the ensemble latent vectors uncovers meaningful classes:

![SEM-EDX latents](assets/images/Suplementary_Figure7.png)  
*Figure 7: Latent clusters from SEM-EDX data.*

### X-ray Computed Tomography

Our approach also works on 3D XCT volumes:

![XCT example](assets/images/Suplementary_Figure6.png)  
*Figure 6: Denoising 3D XCT data.*

Latent clustering highlights structural features:

![XCT latents](assets/images/Figure3.png)  
*Figure 8: Latent clusters from XCT data.*

---

## Datasets

- **Synthetic data**: [phzwart/BTN_Synthetic](https://huggingface.co/datasets/phzwart/BTN_Synthetic)  
- **X-ray CT of soil**: [phzwart/BTN_XCT](https://huggingface.co/datasets/phzwart/BTN_XCT)  
- **SEM-EDX of soil**: [phzwart/BTN_SEM-EDX](https://huggingface.co/datasets/phzwart/BTN_SEM-EDX)  

---

## Code

This research builds on our core libraries:

- [DLSIA (Deep Learning for Scientific Imaging & Automation)](https://github.com/phzwart/dlsia)  
- [qlty (Tensor chunking & stitching for PyTorch)](https://github.com/phzwatr/qlty)  
