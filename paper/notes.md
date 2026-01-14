# Experiment Log (Rice Grain Journal Study)

- Project: Rice grain journal study (VQI + XAI failure analysis + domain robustness)
- Dataset: 38 classes, 500 original/class (19,000 total)
- Split plan: 60/20/20 stratified
- Augmented dataset: NOT used (avoid leakage)
- Model baseline: ResNet50 (ImageNet pretrained)
- Input: 224×224 RGB, ImageNet normalization
- Metrics: accuracy, macro-F1, per-class accuracy, confusion matrix
- Random seed policy: fixed seeds for split + training

## Day 1
- [x] Folder structure created
- [ ] Raw dataset placed in data/raw (original only)
- [ ] Verified class folders = 38
- [ ] Counted images per class (should be 500 each)

### Environment
- OS:
- Python:
- Framework: TensorFlow/Keras
- GPU:
- CUDA/cuDNN (optional):

