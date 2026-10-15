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
| Leaderboard rank | [TODO: rank / number of participants] |

Live leaderboard: [DRV Leaderboard](https://tasneem-mselim.github.io/DRV/)

---

## 🎯 Task

- **Input:** an image from a dashboard camera showing the driver
- **Output:** one of 10 driver activity classes (`0`-`9`)
- **Primary metric:** Macro F1, plus accuracy

Classes (State Farm dataset): [TODO: confirm mapping used in this competition]
safe driving, texting (right), phone (right), texting (left), phone (left), operating the radio, drinking, reaching behind, hair and makeup, talking to passenger.

## 📂 Dataset

[State Farm Distracted Driver Detection](https://www.kaggle.com/datasets/rightway11/state-farm-distracted-driver-detection), organized as `train/` and `test/`.

- Training images used: [TODO: number; the full dataset is much larger than 6,000, so state the subset if you used one]
- Validation strategy: [TODO: ideally split by driver, so validation drivers are unseen in training]
- Rules: CNNs and transfer learning allowed; no external driving datasets.

## 🧠 My Approach

- **Model:** [TODO: exact architecture, e.g. ResNet50 / EfficientNet-B0, pretrained on ImageNet]
- **Preprocessing:** [TODO: resize, normalization]
- **Augmentation:** [TODO: what you used, and why it suits driver images]
- **Training setup:** [TODO: optimizer, learning rate, epochs, batch size, frozen vs fine-tuned layers]
- **Frameworks:** Python, PyTorch / TensorFlow, OpenCV [TODO: keep only what you used]

## 🔬 Analysis

[TODO: add these once you have them]

- Confusion matrix and per-class F1 (which classes are confused, e.g. phone vs texting)
- Gap between validation and hidden-test performance
- Effect of fine-tuning depth and augmentation
- Failure cases: inter-class similarity, occlusion, lighting

## ⚠️ Limitations

- Test accuracy (38.15%) is far below what published methods reach on this dataset. I treat this project as an exploratory study of failure modes rather than a state-of-the-art result.
- Likely contributors [TODO: confirm or remove after your own experiments]: generalization to drivers not seen in training, limited fine-tuning, and visually similar classes.

## 🚀 Reproducing

```bash
git clone https://github.com/Yousif2005/DRV.git
cd DRV
pip install -r requirements.txt   # [TODO: add requirements.txt]
jupyter notebook starter-code-competition.ipynb   # [TODO: or name of your own notebook]
```

## 🗂 Repository Contents

| Path | Description |
| :--- | :--- |
| `starter-code-competition.ipynb` | Starter notebook from the organizer [TODO: link or rename your own notebook] |
| `evaluate.py`, `generate_leaderboard_html.py`, `final_leaderboard.csv`, `index.html` | Competition evaluation and leaderboard (organizer) |
| `submission/`, `encryption/` | Encrypted submission workflow (organizer) |

## 📝 Original Competition Format

Participants submit `submission.csv` with columns `id` (test image name, exactly as provided) and `label` (integer class `0`-`9`), encrypted with the provided script and submitted through a pull request. One submission per participant. Full instructions are in the [upstream repository](https://github.com/tasneem-mselim/DRV).

## 📚 References

- State Farm Distracted Driver Detection, Kaggle.

## 👩‍🏫 Credits

Competition organizer: Tasneem Selim
