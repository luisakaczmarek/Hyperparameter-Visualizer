# Fashion-MNIST Hyperparameter Visualizer

An interactive, browser-based teaching tool that demonstrates how key neural network hyperparameters affect training dynamics — without requiring any model training or Python environment.

---

## Purpose

Understanding *why* hyperparameters matter is difficult from theory alone. This visualiser lets students **change one variable at a time** and immediately observe the effect on training and validation loss/accuracy curves — reinforcing intuitions that would otherwise require hours of GPU compute to build.

The five experiments mirror the structure of the accompanying lab notebook:

| Tab | Hyperparameter | What students learn |
|-----|----------------|---------------------|
| A | Learning Rate | Divergence, slow convergence, and the Goldilocks zone |
| B | Batch Size | Gradient noise as implicit regularisation; speed vs. accuracy trade-off |
| C | Optimizer | SGD vs. momentum vs. adaptive methods (RMSprop, Adam) — including internal update rules |
| D | Architecture | Underfitting, overfitting, depth vs. width, vanishing gradients |
| E | ANN vs. CNN | Inductive bias, local receptive fields, weight sharing |
| F | Optimizer Deep Dive | 7 optimizers on CNN: SGD family vs adaptive family, Adagrad's dying LR, AdamW's decoupled weight decay, Nesterov look-ahead |

Each tab includes:
- Interactive radio controls to select a configuration
- An "Overlay all" toggle for direct side-by-side comparison
- Annotated explanations of the observed behaviour, connecting curve shapes to the underlying mechanism
- Summary statistics (final accuracy, best val loss epoch, train-val gap)

Tab C additionally includes an **Optimizer Internal Mechanisms** panel showing the mathematical update rule for each optimiser (SGD, SGD + Momentum, RMSprop, Adam), key hyperparameter values, and a plain-English description of what each formula does — with the selected optimiser's card highlighted.

Tab F (**Optimizer Deep Dive**) extends Tab C with 7 optimizers all run on the CNN architecture, covering the full SGD family (SGD → SGD+Nesterov) and adaptive family (Adagrad → RMSprop → Adam → AdamW → Nadam). It includes a best-val-accuracy bar chart, per-optimizer annotations connecting internal mechanics to observed curve behaviour, and a 7-card mechanism panel with update rules for all optimizers. Based on the voluntary extension experiment from the course notebook.

---

## How to Use

No installation required. Open the file directly in any modern browser:

```bash
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux
```

Or serve it locally if you prefer:

```bash
python -m http.server 8000
# then visit http://localhost:8000
```

---

## How It Works

All training curves are **mathematically simulated** using a seeded pseudo-random noise model that reproduces realistic deep learning behaviour (exponential decay, overfitting divergence, heteroskedastic noise, vanishing gradient slow-start). No actual model training occurs — the page is fully self-contained with no backend.

The simulation parameters were calibrated against real Fashion-MNIST experiments run on the dataset (TensorFlow 2.x, GPU), so the curve shapes, final accuracy values, and relative orderings reflect genuine empirical outcomes.

---

## Dependencies

| Library | Version | How loaded |
|---------|---------|------------|
| [Chart.js](https://www.chartjs.org/) | 4.4.0 | CDN (no install needed) |

No build step, no package manager, no runtime required.

---

## File Structure

```
.
└── index.html    # entire app — HTML, CSS, and JS in one file
```

---
