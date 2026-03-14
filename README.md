# 🧬 GAN Lab

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Gradio](https://img.shields.io/badge/Gradio-FF7C00?style=for-the-badge&logo=gradio&logoColor=white)
![HuggingFace](https://img.shields.io/badge/HuggingFace-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)
![MNIST](https://img.shields.io/badge/Dataset-MNIST-00C7B7?style=for-the-badge)

### A unified interactive UI for training and exploring Generative Adversarial Networks

**[🚀 Live Demo → GAN Lab on Hugging Face Spaces](https://huggingface.co/spaces/realsuyash/gan-lab)**

</div>

---

## 📌 Overview

**GAN Lab** is an interactive web application built with **Gradio** that lets you explore three GAN architectures trained on the MNIST dataset — all in one place.

- 🎨 **Generate** new handwritten digit images from random noise
- 🔎 **Classify** whether an image is Real or Fake using the Discriminator
- 📈 **Track training progress** with epoch-wise image snapshots and loss curves
- 📊 **Compare** all three models side by side

---

## 🤖 Models

| Model | Architecture | Dataset | Key Feature |
|-------|-------------|---------|-------------|
| **Vanilla GAN** | Fully Connected (FC) layers | MNIST 28×28 | Baseline GAN — simple and fast |
| **CGAN** | FC + Label Embedding | MNIST 28×28 | Conditional generation — control which digit (0–9) to generate |
| **DCGAN** | Transposed Convolutions | MNIST 32×32 | Sharper outputs using spatial conv layers |

---

## 🖥️ App Features

### 🧬 Generate Tab
- Select any of the 3 models
- Choose number of images (1–8)
- For CGAN — select condition label (digit 0–9)
- Download generated images directly

### 🔎 Classify Tab
- Upload any image
- Discriminator returns **Real / Fake** prediction
- Shows confidence score and raw D(x) score

### 📈 Training Progress Tab
- View generated image snapshots saved every 10 epochs
- See how the Generator improves from epoch 10 → 200
- Loss curves for Generator and Discriminator

### 📊 Model Summary Tab
- Live status of all 3 models
- Discriminator accuracy, epochs trained

---

## 🗂️ Project Structure

```
gan-lab/
│
├── 01_vanilla_gan.py       # Vanilla GAN training script
├── 02_cgan.py              # CGAN training script
├── 03_dcgan.py             # DCGAN training script
├── 04_streamlit_colab.py   # Colab launcher (writes app + runs tunnel)
├── gan_gradio.py           # Gradio app writer cell
│
├── app.py                  # Main Gradio app (deployed to HF Spaces)
├── requirements.txt        # Dependencies
│
├── vanilla_gan.pth         # Trained Vanilla GAN weights
├── cgan.pth                # Trained CGAN weights
├── dcgan.pth               # Trained DCGAN weights
│
└── epoch_imgs/
    ├── Vanilla_GAN/        # epoch_010.png ... epoch_200.png
    ├── CGAN/
    └── DCGAN/
```

---

## ⚡ Quickstart (Google Colab)

### Step 1 — Install
```python
!pip install gradio torch torchvision -q
```

### Step 2 — Train all 3 models
Run the training cells in order:
- `01_vanilla_gan.py` → saves `vanilla_gan.pth`
- `02_cgan.py` → saves `cgan.pth`
- `03_dcgan.py` → saves `dcgan.pth`

> 💡 Use **T4 GPU** runtime for best speed (Runtime → Change runtime type → T4 GPU)

### Step 3 — Run the app locally
```python
import subprocess, sys
subprocess.run([sys.executable, "gan_app.py"])
```

Gradio prints a public `gradio.live` link — click it to open the app.

---

## 🚀 Deploy to Hugging Face Spaces

```python
from huggingface_hub import HfApi, notebook_login

notebook_login()
api = HfApi()

# Upload app
api.upload_file(path_or_fileobj="gan_app.py", path_in_repo="app.py",
                repo_id="your-username/gan-lab", repo_type="space")

# Upload weights
for f in ["vanilla_gan.pth", "cgan.pth", "dcgan.pth"]:
    api.upload_file(path_or_fileobj=f, path_in_repo=f,
                    repo_id="your-username/gan-lab", repo_type="space")
```

---

## 📦 Requirements

```
torch
torchvision
gradio
matplotlib
numpy
Pillow
```

---

## 🧪 Training Details

| Config | Vanilla GAN | CGAN | DCGAN |
|--------|------------|------|-------|
| Epochs | 200 | 200 | 200 |
| Batch Size | 128 | 128 | 128 |
| Latent Dim | 100 | 100 | 128 |
| Optimizer | Adam (β=0.5) | Adam (β=0.5) | Adam (β=0.5) |
| LR | 2e-4 | 2e-4 | 2e-4 |
| Loss | BCELoss | BCELoss | BCELoss |
| Image Size | 28×28 | 28×28 | 32×32 |

---

## 📸 Screenshots

> Generate Tab — CGAN generating digit samples

> Training Progress — DCGAN improvement from epoch 10 to 200

> Model Summary — all 3 models loaded and ready

---

## 🔗 Links

- 🤗 **Live App** → [GAN Lab on Hugging Face Spaces](https://huggingface.co/spaces/realsuyash/gan-lab)
- 📓 **Colab Notebook** → *will be publish soon*
- 👤 **Author** → [realsuyash](https://huggingface.co/realsuyash)

---

## 📚 References

- [Goodfellow et al., 2014 — Generative Adversarial Nets](https://arxiv.org/abs/1406.2661)
- [Mirza & Osindero, 2014 — Conditional GAN](https://arxiv.org/abs/1411.1784)
- [Radford et al., 2015 — DCGAN](https://arxiv.org/abs/1511.06434)

---

<div align="center">

Made with ❤️ · MTech AI/ML · COEP Technological University, Pune

</div>
