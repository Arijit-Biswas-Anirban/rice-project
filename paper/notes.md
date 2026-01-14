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
- [x] Raw dataset placed in data/raw (original only)
- [x] Verified class folders = 38
- [x] Verified images/class = 500 (total 19000)
- [x] Created stratified splits (60/20/20) with fixed seed = 20260115
- [x] Verified splits: per-class counts (300/100/100), no overlap, existence check PASS

## Day 2
- [x] Loaded train/val/test CSV splits inside TensorFlow
- [x] Created deterministic label-to-id mapping (38 classes)
- [x] Built tf.data pipeline from CSV filepaths
- [x] Image decoding, resizing (224x224), ImageNet normalization applied
- [x] Enabled GPU acceleration (RTX 3050 confirmed)
- [x] Verified batch shapes and label correctness
- [x] Visual sanity check passed (images look correct after unnormalization)

## Day 3
- [x] Trained ResNet50 baseline with frozen backbone
- [x] Achieved validation accuracy ≈ 0.49
- [x] Test accuracy = 0.4795
- [x] Macro-F1 = 0.4616 (38-class evaluation)
- [x] Generated normalized confusion matrix
- [x] Identified high-performing and low-performing classes
- [x] Observed structured confusion among visually similar rice varieties




### Environment
- OS: Ubuntu 24.04
- Python: 3.10.13
- Framework: TensorFlow 2.20.0 (Keras)
- GPU: NVIDIA GeForce RTX 3050
- Environment: conda env "tf310" (miniforge)
- CUDA/cuDNN: ~1400+

