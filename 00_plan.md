# Phase 1 — Project Plan: Fashion-MNIST Clothing Classifier

**Student:** Mohammed Alosaily  
**Dataset:** Fashion-MNIST  
**Date:** 2026-06-06

---

## 1. Problem Statement

We want to **automatically classify clothing images** for fashion retail companies so that **product inventory tagging can be automated without manual effort**, by building a CNN model that **identifies 10 clothing categories (T-shirt, Trouser, Pullover, Dress, Coat, Sandal, Shirt, Sneaker, Bag, Ankle boot) from 28×28 grayscale images**.

---

## 2. Success Metrics

### Technical Metrics
| Metric | Target |
|--------|--------|
| Test accuracy | ≥ 92% |
| Inference time | < 100 ms per image |
| Validation accuracy gap (train vs val) | < 2% (no overfitting) |

### Business Metric
- Automate **90% of product image tagging** without human review, reducing manual labelling cost for a fashion retailer.

---

## 3. Data Needs

| Property | Detail |
|----------|--------|
| Source | `keras.datasets.fashion_mnist` (built-in, no download needed) |
| Format | Grayscale PNG-like arrays, 28×28 pixels, uint8 |
| Size | 70,000 images total — 60,000 train, 10,000 test |
| Classes | 10 balanced classes (~6,000–7,000 images each) |
| License | MIT License (Zalando Research, open for academic use) |

**Class Labels:**

| Label | Class |
|-------|-------|
| 0 | T-shirt/top |
| 1 | Trouser |
| 2 | Pullover |
| 3 | Dress |
| 4 | Coat |
| 5 | Sandal |
| 6 | Shirt |
| 7 | Sneaker |
| 8 | Bag |
| 9 | Ankle boot |

---

## 4. Risks & Mitigations

| # | Risk | Likelihood | Impact | Mitigation |
|---|------|------------|--------|------------|
| 1 | **Overfitting** — model memorises training data but fails on test set | High | High | Add Dropout layers (0.25–0.5); use early stopping; monitor val accuracy each epoch |
| 2 | **Visually similar classes** — Shirt vs T-shirt, Coat vs Pullover are hard to distinguish even for humans | High | Medium | Use deeper CNN; analyse confusion matrix carefully; report per-class F1 scores |
| 3 | **Distribution gap** — Fashion-MNIST uses clean, centered studio images; real product photos are messy, rotated, and variable in lighting | Medium | High | Document as a known limitation in the report; add data augmentation (rotations, flips) as a future step |
| 4 | **Package version conflicts** — TensorFlow/Keras API changes between versions | Low | Medium | Pin all package versions in `requirements.txt`; test with `Restart & Run All` before submission |

---

## 5. Project Architecture Plan

```
Phase 2 — Training (01_train.ipynb)
  ├── Load Fashion-MNIST via keras.datasets
  ├── Normalize pixels (0–255 → 0.0–1.0)
  ├── Add channel dimension: (28,28) → (28,28,1)
  ├── Split: 54,000 train / 6,000 val / 10,000 test (untouched)
  ├── CNN: Conv2D(32) → MaxPool → Conv2D(64) → MaxPool → Dense(128) → Dense(10)
  ├── Experiments: baseline → +Dropout → +more epochs
  └── Save model to models/fashion_cnn.h5

Phase 3 — Evaluation (02_evaluate.ipynb)
  ├── Load saved model
  ├── Run model.evaluate() on test set (one time only)
  ├── Classification report (precision, recall, F1 per class)
  ├── Confusion matrix 10×10 → reports/confusion_matrix.png
  ├── Error analysis: 9 misclassified images
  └── Training curves → reports/training_curves.png

Phase 4 — Report (report.md)
  └── 5-part story: Problem → Approach → Results → Analysis → Next Steps

Phase 5 — Package (requirements.txt + reflection)
  └── Pinned versions, clean repo, reflection
```

---

## 6. Timeline

| Day | Phase | Deliverable |
|-----|-------|-------------|
| Day 46 | Phase 1 — Plan | `00_plan.md` |
| Day 47 | Phase 2 — Train | `notebooks/01_train.ipynb`, `models/fashion_cnn.h5` |
| Day 48 | Phase 3 — Evaluate | `notebooks/02_evaluate.ipynb`, `reports/*.png` |
| Day 49 | Phase 4 — Present | `report.md` |
| Day 50 | Phase 5 — Submit | `requirements.txt`, final zip |
