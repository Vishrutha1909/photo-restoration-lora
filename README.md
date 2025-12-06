# photo-restoration-lora
AI project to restore damaged photographs using LoRA fine-tuned diffusion models.

# Team Members 

Akshara Y Tarikere - Github Username: aksharayt

Anshu Reddy Ashanna - Github Username: AnshuReddyAshanna

Vishrutha Ravi - Github Username: Vishrutha1909

# Project Summary

This project focuses on developing an AI model that can automatically restore damaged or old photographs. Many old family photos are affected by scratches, stains, fading, and other forms of visual deterioration, and restoring those images will be expensive. Our goal is to create an accessible and cost-effective solution that can bring these photos back to life using modern deep learning techniques.

We use LoRA (Low Rank Adaptation) for fine-tuning a Stable Diffusion model so that it can learn how to restore damaged images and recover their original appearance. LoRA allows us to adapt large diffusion models efficiently by training only small, low-rank updates instead of all the model parameters. This approach keeps the computational cost low and works well on free GPU resources available in Google Colab.

To train the model, we plan to collect about 50 to 100 clean photographs. We then generate synthetic damage on these images by adding scratches, tears, stains, and fading effects. The model is trained to map the damaged images back to their clean versions, which helps it learn the restoration process effectively.

We evaluate the performance of our restoration system using both quantitative and qualitative measures. We aim for a PSNR (Peak Signal to Noise Ratio) score above 25 dB and an SSIM (Structural Similarity Index) score above 0.85, which indicates strong similarity between the restored photo and the original. In addition to these metrics, the restored images should look natural and visually convincing to human observers.

The final objective of this project is to build a practical and easy to use model that can restore old photos with high quality results, giving users a way to preserve valuable memories without the high cost or time required for manual restoration.

# Dataset and weights Google Drive Link

Vishrutha Ravi : https://drive.google.com/drive/folders/1bg7aNY4oXFHML9ftcPs0fFeGRfVwS4-G?usp=sharing

Anshu Reddy Ashanna : https://drive.google.com/drive/folders/1C7zpzlm54kThb-iFJ97yzmDUtZkqNFLy?usp=sharing

# Folder Structure

```
Photo-Restoration-LoRA/
│
├── Dataset/
│   ├── raw Images/
│   └── damaged images/
│
├── metrics/
│   ├── psnr_scores.csv
│   └── ssim_scores.csv
│
├── notebooks/
│   ├── Photo_Restoration_LoRA_Vishrutha.ipynb
│   ├── Preprocessing.ipynb
│   ├── damage_images.ipynb
│   ├── photo_restoration_lora_preprocessing.ipynb
│   └── training_and_eval_notebook_1.ipynb
│
├── plots/
│   ├── Distribution of PSNR Improvement.png
│   ├── PSNR Comparison.png
│   ├── PSNR Distribution Comparison.png
│   └── SSIM Comparison.png
│
├── results/
│   ├── Final Restored (LoRA).png
│   └── Restored (LoRA).png
│
├── .gitignore
├── Project Deliverable 1.pdf
├── README.md
└── requirements.txt
```
# Data Description

## Dataset Type:

Real clean photographs

Real damaged photographs

Automatically generated crack & damage masks

## Dataset Size:

Total aligned samples: 109 image pairs

Image resolution: 512 × 512

# Methodology

## Preprocessing

The following steps are applied to all images:

- Center cropping to square format

- Resizing to 512 × 512

- Histogram equalization for contrast normalization

- PNG format standardization

These steps ensure consistent training input for the diffusion model.

## Automatic Damage Mask Generation

Damage masks are created automatically using computer vision techniques:

- LAB color space conversion

- Laplacian filtering for crack detection

- Bright region thresholding for paint loss

- Morphological noise removal

- Area-based filtering

- Gaussian feathering for soft museum-grade masks

This makes the pipeline fully automated with zero manual labeling.

# Modeling Approach

1. Base Model

Stable Diffusion Inpainting Model

runwayml/stable-diffusion-inpainting

2. LoRA Fine-Tuning

LoRA adapters attached only to UNet attention layers

Frozen components:

- VAE

- Text encoder

Trainable parameters: ~0.37% of total model

Training details:

- Epochs: 5

- Batch size: 1

- Learning rate: 1e-5

- Optimizer: AdamW

Loss: Mask-weighted MSE loss in latent space

# Restoration Inference Pipeline

Input:

- Damaged image

- Auto-generated damage mask

Process:

- Prompt-guided inpainting using LoRA-enhanced diffusion

- Strength and guidance control

## Final blending:

Final Output = Restored × Mask + Original × (1 − Mask)

This ensures only damaged regions are modified while preserving identity and texture.

# Evaluation Metrics

The model is evaluated using:

- PSNR (Peak Signal-to-Noise Ratio) → Pixel reconstruction quality

- SSIM (Structural Similarity Index) → Structural & perceptual similarity

## Final Results (50 Random Samples):

Damaged  → Clean | PSNR: 13.59 | SSIM: 0.3827
Restored → Clean | PSNR: 13.75 | SSIM: 0.4066

## TRUE IMPROVEMENT:

PSNR Gain : +0.16 dB
SSIM Gain : +0.0240

These results confirm quantitative restoration improvement.

# Links to datasets

https://www.kaggle.com/datasets/bharatadhikari/humanface8000

https://www.kaggle.com/datasets/pes1ug22am047/damaged-and-undamaged-artworks
