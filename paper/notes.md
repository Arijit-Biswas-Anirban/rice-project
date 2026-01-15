# Experiment Log (Rice Grain Journal Study)

- Project: Rice grain journal study (VQI + XAI failure analysis + domain robustness)
- Dataset: 38 classes, 500 original/class (19,000 total)
- Split plan: 60/20/20 stratified
- Augmented dataset: NOT used (avoid leakage)
- Model baseline: ResNet50 (ImageNet pretrained)
- Input: - Input: 224×224 RGB, ImageNet mean/std normalization (mean=[0.485,0.456,0.406], std=[0.229,0.224,0.225])
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

## Day 4
- [x] Loaded baseline model from `experiments/exp001_baseline_resnet50/best_model.keras`
- [x] Reproduced Day 3 performance on test set (accuracy ≈ 0.4795)
- [x] Critical fix: confirmed training-time preprocessing = ImageNet mean/std normalization  
      (mean=[0.485,0.456,0.406], std=[0.229,0.224,0.225]); `preprocess_input` caused mismatch
- [x] Built `pred_df` with: y_true, y_pred, true_name, pred_name, p_true, p_pred, is_correct
- [x] Visualized:
  - correct vs wrong counts
  - confidence distribution (p_pred) for correct vs wrong
- [x] Generated labeled normalized confusion matrix (row-normalized) with value overlay
- [x] Extracted top confusion pairs (true → pred) by row-normalized error rate
- [x] Created Grad-CAM case list: `outputs/xai/gradcam/selected_cases.csv`
  - total = 152 (wrong_pair=80, correct_ref=72)
- [x] Implemented Grad-CAM using manual forward path (backbone + head) to avoid nested-model gradient issues
- [x] Saved Grad-CAM panels:
  - `outputs/xai/gradcam/panels/` (152 images; 3-panel: original, pred-CAM, true-CAM)
- [x] Computed Grad-CAM quantitative summaries:
  - entropy saved: `outputs/xai/gradcam/gradcam_metrics.csv`
  - peakiness (top-5% mass) saved: `outputs/xai/gradcam/gradcam_peakiness.csv`
- [x] Identified extreme wrong cases by high true-CAM peakiness:
  - `outputs/xai/gradcam/extreme_wrong_cases.csv`
  - example panels saved: `outputs/xai/gradcam/extreme_panels/`



### Environment
- OS: Ubuntu 24.04
- Python: 3.10.13
- Framework: TensorFlow 2.20.0 (Keras)
- GPU: NVIDIA GeForce RTX 3050
- Environment: conda env "tf310" (miniforge)
- CUDA/cuDNN: ~1400+

