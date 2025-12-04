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

https://drive.google.com/drive/folders/1bg7aNY4oXFHML9ftcPs0fFeGRfVwS4-G?usp=sharing

# Notebook Links

https://colab.research.google.com/drive/16zK69ifQ8g_WIXN388HB7G2EEgB2TLi-?usp=sharing

https://colab.research.google.com/drive/1LCnyFeI6fOS5Lfwu5DRsZRWtT5Cldhqk?usp=sharing

# Links to datasets
https://www.kaggle.com/datasets/bharatadhikari/humanface8000

https://www.kaggle.com/datasets/pes1ug22am047/damaged-and-undamaged-artworks
