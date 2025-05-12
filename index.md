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

Scanning Electron Microscopy with Energy Dispersive X-ray spectroscopy (SEM-EDX) is a rich analytical technique that provide qualitative insights in material composition, revealing structure and elemental composition. Collecting data can be time-intensive though, especially when you want to have really good resolution and good signal to noise. Here we investigate if we can learn an efficient denoisier on limited data, and use this to clean up large section images that normalluy would take weaks to measure at decent noise levels. We start with a small patch. The high-noise image took 7 seconds to collect, the low noise one took 2 hours. The data consists of 3 channels, measuring the Si, Al and Fe content. Our training data consists of 10 7 second images of the patch below, and a single 2 hour image of the same area. 

![SEM-EDX example](assets/images/Suplementary_Figure3.png)  
*Figure 4: SEM-EDX training data.*

The denoising is of course not a detailed as the 2 hour image, but we can get a good idea of what is going on 

On unseen samples, denoising yields clear material contrasts:

![SEM-EDX example](assets/images/Figure2.png)  
*Figure 5: Denoising SEM-EDX results on unseen data.*

Inspecting the predicted quantile levels for the Fe channel, allows us to make good estimates of where potential, regions of interest are to re-measure at longer count rates. 
![SEM-EDX FE example](assets/images/Suplementary_Figure5.png)  

It turns out that when we cluster the ensemble latent vectors of our networks, we un uncover meaningful classes:

![SEM-EDX latents](assets/images/Suplementary_Figure7.png)  
*Figure 7: Latent clusters from SEM-EDX data.*


### X-ray Computed Tomography

Our approach also works on 3D XCT volumes. Here we denoise a fast collected dataset given one that was collected at lower throughput, with more frames. We use 3D variants of the networks used above, to make sure that we can fully utilize the 3D nature of the data.

![XCT example](assets/images/Suplementary_Figure6.png)  
*Figure 6: Denoising 3D XCT data.*

Again, when we cluster our latent vectors, we highlights structural features:

![XCT latents](assets/images/Figure3.png)  
*Figure 8: Latent clusters from XCT data.*

---

## Conclusions

What began as a simple denoising tool has revealed a much richer story: by cleaning up noisy images we don’t just recover clearer signals—we uncover hidden, semantic structure in the data. The calibrated denoising we demonstrate can guide more efficient experimental designs, while the emergent clusters in latent space point to where manual annotations or downstream analyses should focus.  

For a deeper dive into methods and results please see the full paper.  


## Datasets

- **Synthetic data**: [phzwart/BTN_Synthetic](https://huggingface.co/datasets/phzwart/BTN_Synthetic)  
- **X-ray CT of soil**: [phzwart/BTN_XCT](https://huggingface.co/datasets/phzwart/BTN_XCT)  
- **SEM-EDX of soil**: [phzwart/BTN_SEM-EDX](https://huggingface.co/datasets/phzwart/BTN_SEM-EDX)  

---

## Code

This research builds on our core libraries:

- [DLSIA (Deep Learning for Scientific Imaging & Automation)](https://github.com/phzwart/dlsia)  
- [qlty (Tensor chunking & stitching for PyTorch)](https://github.com/phzwatr/qlty)  
