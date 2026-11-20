# Benchmarking Deepfake Detectors on Diffusion-Generated Images

A controlled comparison of five deepfake detectors — CNNDetect, EfficientNet-B4, CLIP with LoRA, DIRE, and FIRE — for spotting diffusion-generated images (Midjourney, Stable Diffusion). Each model is evaluated zero-shot and after architecture-specific fine-tuning, on identical in-distribution splits drawn from OpenFake and on an out-of-distribution set of images from 18 unseen generators. CLIP+LoRA is the strongest and most robust detector, and the only one to generalize meaningfully beyond the generators seen in training.

Course project for CMP603 Advanced Computer Vision, Cairo University. The paper (PDF and LaTeX source) is in `Paper/`.

## Structure

```
Code/
  ID & OOD Dataset Creation/   build the ID and OOD sets from OpenFake
  CLIP + LoRA/                 zero-shot, fine-tune, and OOD notebooks
  CNN Detect/                  (same pattern per model)
  DIRE/
  EfficientNet/
  FIRE/
Dataset/                       dataset links
Paper/                         LaTeX source + PDF
```

## Running it

The notebooks run on Google Colab (T4 GPU). The in-distribution and out-of-distribution sets are built from OpenFake — links are in `Dataset/Datasets Links.txt`. Each notebook installs its own dependencies in its first cells; the common core is:

```bash
pip install torch torchvision timm transformers peft scikit-learn
```

DIRE, FIRE, and CNNDetect additionally pull their original repositories and pretrained checkpoints, as noted in their notebooks.

1. `Code/ID & OOD Dataset Creation/` — assemble and split the data (80/10/10, seed 42).
2. `Code/<model>/` — run that model's zero-shot, fine-tuning, and OOD evaluation notebooks.

Models are selected by validation AUC; all splits use seed 42.

## Results

Fine-tuned macro F1 and ROC AUC on the in-distribution (ID) and out-of-distribution (OOD) test sets (percentages):

| Model | ID macro F1 | ID AUC | OOD macro F1 | OOD AUC |
|---|---|---|---|---|
| CNNDetect | 84.97 | 93.80 | 53.61 | 57.90 |
| EfficientNet-B4 | 87.49 | 95.12 | 46.98 | 48.00 |
| CLIP+LoRA | 94.34 | **99.21** | 56.12 | **83.45** |
| DIRE | 64.67 | 70.63 | 41.14 | 33.54 |
| FIRE | 64.50 | 73.20 | 45.00 | 43.37 |

No model detects reliably zero-shot. After fine-tuning, CLIP+LoRA is strongest in-distribution and the only model to retain meaningful separability on unseen generators; the reconstruction-based detectors DIRE and FIRE fall below chance AUC out-of-distribution, showing that strong in-distribution accuracy does not imply real-world robustness.

Licensed under MIT.

## Contributors

| [<img src="https://github.com/FatemaKotb.png" width="80" alt="Fatema Kotb"/><br/>Fatema Kotb](https://github.com/FatemaKotb) | [<img src="https://github.com/BasmaElhoseny01.png" width="80" alt="Basma Elhoseny"/><br/>Basma Elhoseny](https://github.com/BasmaElhoseny01) | [<img src="https://github.com/mennamohamed0207.png" width="80" alt="Menna Mohamed"/><br/>Menna Mohamed](https://github.com/mennamohamed0207) | [<img src="https://github.com/khadija2-2.png" width="80" alt="Khadija"/><br/>Khadija](https://github.com/khadija2-2) | Habiba Assem |
|:-:|:-:|:-:|:-:|:-:|