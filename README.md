# Jailbreaking Deep Models: Adversarial Evaluation of ResNet-34 on ImageNet

## 📌 Overview

This project investigates the adversarial robustness of a pretrained ResNet-34 model trained on the ImageNet-1K dataset. We implement and evaluate the impact of several adversarial attack techniques including:

- **Fast Gradient Sign Method (FGSM)**
- **Projected Gradient Descent (PGD)**
- **Patch-based Momentum Iterative FGSM (MI-FGSM)**

We also explore the **transferability** of adversarial examples to a different architecture, **DenseNet-121**, to analyze cross-model vulnerabilities. All experiments are built using PyTorch and executed under white-box assumptions.

## 📁 Project Structure

```
.
├── attacks/
│   ├── fgsm.py
│   ├── pgd.py
│   └── patch_attack.py
├── models/
│   ├── resnet34.py
│   └── densenet121.py
├── data/
│   ├── imagenet_subset/
│   └── labels_list.json
├── notebooks/
│   └── evaluation_pipeline.ipynb
├── utils/
│   ├── evaluation.py
│   └── visualization.py
├── results/
│   ├── fgsm/
│   ├── pgd/
│   └── patch/
├── requirements.txt
└── README.md
```

## 🧪 Attacks Implemented

### 1. FGSM (Fast Gradient Sign Method)
- Single-step, fast and efficient
- Perturbation budget: \( \epsilon = 0.02 \)

### 2. PGD (Projected Gradient Descent)
- Iterative extension of FGSM
- Perturbation budget: \( \epsilon = 0.02 \), step size \( \alpha = 0.005 \), 10 iterations

### 3. Patch-based MI-FGSM
- Perturbation confined to a 32×32 region
- Budget: \( \epsilon \in [0.3, 0.5] \)
- Variants include random, fixed, and saliency-guided placements

## 📊 Results Summary

| **Model**       | **Attack** | **Top-1 Accuracy** | **Top-5 Accuracy** |
|----------------|------------|--------------------|--------------------|
| ResNet-34      | Baseline   | 76.00%             | 94.20%             |
|                | FGSM       | 6.40%              | 33.00%             |
|                | MI-FGSM    | 0.00%              | 12.00%             |
|                | Patch      | 9.00%              | 42.60%             |
| DenseNet-121   | Baseline   | 74.80%             | 93.60%             |
|                | FGSM       | 51.00%             | 79.00%             |
|                | MI-FGSM    | 46.40%             | 79.80%             |
|                | Patch      | 60.20%             | 87.80%             |

## 🚀 Running the Code

### Environment Setup

```bash
conda create -n adv-env python=3.7
conda activate adv-env
pip install -r requirements.txt
```

### Example Commands

```bash
# FGSM Attack
python attacks/fgsm.py --epsilon 0.02

# PGD Attack
python attacks/pgd.py --epsilon 0.02 --alpha 0.005 --steps 10

# Patch-based Attack
python attacks/patch_attack.py --epsilon 0.3 --patch_size 32 --mode random
```

## 🔬 Key Contributions

- Implemented reproducible adversarial attack pipeline on ImageNet subset.
- Quantified vulnerability of ResNet-34 and DenseNet-121 under white-box settings.
- Demonstrated high transferability of patch-based attacks.
- Provided visualizations and saved adversarial datasets for benchmarking.

## 📷 Visual Examples

![FGSM Attack](results/fgsm/sample1.png)
![Patch Attack](results/patch/sample2.png)

## 📚 References

- Goodfellow et al., *Explaining and Harnessing Adversarial Examples*, ICLR 2015
- Madry et al., *Towards Deep Learning Models Resistant to Adversarial Attacks*, ICLR 2018
- Dong et al., *Boosting Adversarial Attacks with Momentum*, CVPR 2018

## 👥 Authors

- Nikhil Bhise (nb4053@nyu.edu)  
- Vishwas Karale (vbk2750@nyu.edu)  
- Hemanth Sree Meka (hm3324@nyu.edu)
