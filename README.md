# 🚗 Driver Behavior Detection

10-class image classification of distracted driving behaviors using CNNs and transfer learning.

> This repository is my fork of the class competition repo by [Tasneem Selim](https://github.com/tasneem-mselim/DRV). The competition infrastructure (evaluation scripts, leaderboard, submission encryption) belongs to the organizer. The model, experiments, and analysis described below are my own work.

---

## 📊 Results

Final result on the competition's hidden test set (one submission allowed):

| Metric | Score |
| :--- | :---: |
| Accuracy | **38.15%** |
| Macro F1-score | **36.20** |
| Random-guess baseline (10 classes) | ~10% |


Live leaderboard: [DRV Leaderboard](https://tasneem-mselim.github.io/DRV/)

---

## 🎯 Task

- **Input:** an image from a dashboard camera showing the driver
- **Output:** one of 10 driver activity classes (`0`-`9`)
- **Primary metric:** Macro F1, plus accuracy


## 📂 Dataset

[State Farm Distracted Driver Detection](https://www.kaggle.com/datasets/rightway11/state-farm-distracted-driver-detection), organized as `train/` and `test/`.

- Training images used: 13,936 (11,153 training / 2,783 validation), 10 classes
- Validation strategy: random 80/20 image-level split (not split by driver; see Analysis)
- Rules: CNNs and transfer learning allowed; no external driving datasets.

## 🧠 My Approach

- **Model:** custom CNN trained from scratch (no pretrained weights): 3 × [Conv2D (32/64/128 filters, 3×3, ReLU) + MaxPool], Flatten, Dense(128) + Dropout(0.5), softmax over 10 classes.
- **Input / preprocessing:** images resized to 128×128 and rescaled to [0, 1]. No data augmentation.
- **Training:** Adam (lr = 0.001), batch size 16, up to 10 epochs, early stopping on validation loss (patience 3), seed 25. About 26 minutes on a Kaggle notebook.
- **Validation:** random 80/20 split of the training images (11,153 train / 2,783 validation).
- **Framework:** Python, TensorFlow/Keras, NumPy, pandas, Matplotlib.

## 🔬 Analysis

Validation accuracy reached about **99%** (e.g. 99.43% at epoch 6), while the hidden test accuracy was **38.15%**. A gap this large almost certainly means the validation set was not independent of the training set: the State Farm images come from video frames of a limited number of drivers, so a random image-level split puts near-duplicate frames of the same driver in both training and validation. The model likely learned to recognize drivers and their surroundings, not only behaviors, and this did not generalize to the unseen drivers in the test set. 

Planned improvements:

- Split validation by driver so it measures generalization to new drivers.
- Use a pretrained backbone (e.g. ResNet / EfficientNet) with fine-tuning.
- Add augmentation (crops, brightness, small rotations).
- Report a confusion matrix and per-class F1.

## ⚠️ Limitations

- The reported validation accuracy (~99%) is not a reliable estimate of real performance, for the reason above. The hidden-test result (38.15% accuracy, 36.20 Macro F1) is the honest number.
- No augmentation or transfer learning was used in this version.
- This is a competition project and a first baseline, not a state-of-the-art result.

## 🚀 Reproducing

```bash
git clone https://github.com/Yousif2005/DRV.git
cd DRV
pip install -r requirements.txt   # [TODO: add requirements.txt]
# open and run your notebook (Kaggle notebook: image-project.ipynb)
```

## 🗂 Repository Contents

| Path | Description |
| :--- | :--- |
| `image-project.ipynb` |  Jupyter Notebook 
| `evaluate.py`, `generate_leaderboard_html.py`, `final_leaderboard.csv`, `index.html` | Competition evaluation and leaderboard (organizer) |
| `submission/`, `encryption/` | Encrypted submission workflow (organizer) |

## 📝 Original Competition Format

Participants submit `submission.csv` with columns `id` (test image name, exactly as provided) and `label` (integer class `0`-`9`), encrypted with the provided script and submitted through a pull request. One submission per participant. Full instructions are in the [upstream repository](https://github.com/tasneem-mselim/DRV).

## 📚 References

- State Farm Distracted Driver Detection, Kaggle.

## 👩‍🏫 Credits

Competition organizer: Tasneem Selim
