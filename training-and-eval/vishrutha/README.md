## Photo Restoration using LoRA-Fine-Tuned Stable Diffusion

Focused on developing a LoRA-based Stable Diffusion inpainting framework for automated photo and artwork restoration. The goal is to restore old, damaged, or degraded images by removing cracks, surface damage, and missing paint while preserving the original identity, lighting, and structure.

Instead of full fine-tuning, Low-Rank Adaptation (LoRA) is used to efficiently train only a small subset of model parameters, enabling high-quality restoration using limited data and constrained GPU resources.

## Highlights

1.LoRA fine-tuning of Stable Diffusion Inpainting UNet

2.Mask-guided restoration in latent space

3.Automatic crack mask generation using OpenCV during inference

4.Quantitative evaluation using PSNR & SSIM

5.Qualitative visual comparison (Damaged → Mask → Restored → Clean)

6.Fully reproducible with requirements.txt

## Dataset and weights Google Drive Link

https://drive.google.com/drive/folders/1bg7aNY4oXFHML9ftcPs0fFeGRfVwS4-G?usp=sharing

## Folder Structure

```
vishrutha/
│
├── metrics/
│   ├── psnr_scores.csv
│   └── ssim_scores.csv
│
├── notebooks/
│   ├── Photo_Restoration_LoRA_Final_Vishrutha.ipynb
│   └── training_and_eval_notebook1.ipynb
│
├── plots/
│   ├── Distribution of PSNR Improvement.png
│   ├── PSNR Bar Chart.png
│   ├── PSNR Distribution Comparison.png
│   └── SSIM Bar Chart.png
│
├── results/
│   ├── Final Restored (LoRA).png
│   └── Restored (LoRA).png
│
├── README.md
└── requirements.txt
```



## Methodology

1. Model Setup

Base Model: runwayml/stable-diffusion-inpainting

LoRA is attached to the UNet attention layers:

- to_q, to_k, to_v, to_out.0

Only LoRA weights are trained → memory-efficient fine-tuning

2. Dataset

A pre-aligned dataset of:

- Clean images

- Damaged images

- Corresponding binary masks

- Total training samples: 109 aligned triplets

- No separate synthetic damage pipeline was created. Pre-existing aligned data was directly used for training and evaluation.

3. Training

- LoRA loaded into FP32 for training

- Latent-space training using VAE encodings

- Noise injected using DDPMScheduler

- Mask-weighted MSE loss to focus restoration only on damaged regions

- Optimizer: AdamW

- Learning rate: 1e-5

- Epochs: 5

4. Inference

- LoRA weights loaded into FP16 Stable Diffusion

- Automatic mask generation during testing using OpenCV:

- Black-hat filtering

- Adaptive thresholding

- Morphological filtering

- Gaussian feathering

- Mask-guided inpainting applied during inference

## Evaluation Metrics

Quantitative evaluation was performed using 50 randomly sampled test images.

Metric	Damaged → Clean	Restored → Clean	Gain
PSNR	13.59 dB	13.75 dB	+0.16 dB
SSIM	0.3827	0.4066	+0.0240

## Individual sample scores are saved in:

metrics/psnr_scores.csv

metrics/ssim_scores.csv


## Final visual results are saved in:

results/Final Restored (LoRA).png

results/Restored (LoRA).png

## Installation & Setup

1. Install dependencies
pip install -r requirements.txt

3. Run the main notebook

notebooks/Photo_Restoration_LoRA_Final_Vishrutha.ipynb

## Key Results

Demonstrated that LoRA fine-tuning is effective for restoration with very limited data

## Successfully applied:

- Mask-guided latent diffusion training

- Automatic crack-based inference masking

- Achieved consistent improvement across 50 samples

## Limitations

- Small dataset (109 samples) limits generalization

- Modest numeric gains in PSNR and SSIM

- No multi-condition training (folds, tears, blur, noise)

- Limited training epochs due to GPU constraints

## Future Work

- Expand training dataset.

- Train multi-condition LoRA for:

- Tears

- Folds

- Motion blur

- Severe occlusion

- Extend training to higher resolutions


## Author

Vishrutha Ravi

