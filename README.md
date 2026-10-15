# Hybrid Quantum-Classical CNN for Traffic Sign Classification

This project explores a hybrid quantum-classical convolutional neural network (QC-CNN) for
classifying traffic signs from the **German Traffic Sign Recognition Benchmark (GTSRB)**. The
implementation is provided as Jupyter notebooks and compares a quantum model with classical CNN
baselines.

The work is based on Fan, Shi, Guggemos, and Zhu, *“Hybrid Quantum-Classical Convolutional Neural
Network Model for Image Classification,”* IEEE Transactions on Neural Networks and Learning
Systems, 35(12), 2024. This project applies the approach to a six-class subset of GTSRB rather than
the paper's earth-observation datasets: Priority road, Yield, Stop, No entry, Turn right ahead,
and Keep right.

## Project at a glance

The main experiment uses 16×16 grayscale images and a 13-qubit quantum circuit:

1. GTSRB images are loaded, cropped/preprocessed, converted to grayscale, and resized.
2. The QC-CNN uses FRQI image encoding, three quantum convolution layers, and Pauli X/Y/Z
   measurements.
3. The measured features are passed to a classical dense classifier.
4. Classical CNN baselines and additional experiments compare model performance and behavior.

The 16×16 model has `n = 4`, `m = 3` quantum convolution layers, and `k = 1` kernel-index bit.
Its qubit count is `2n + k + m + 1 = 13`. With X, Y, and Z measurements, the model produces
24 measured features.

## Notebooks

| Notebook | Purpose |
| --- | --- |
| [`final_code-py.ipynb`](./final_code-py.ipynb) | **Main experiment.** 16×16 input, three quantum convolution layers, two kernels per layer, and XYZ measurements. Includes classical baselines, training/evaluation, and analysis sections. |

This repository intentionally publishes only the primary experiment notebook. Additional
measurement-basis and resolution variants from the working directory are excluded to keep the
initial GitHub repository focused.

## Dataset

The notebooks expect the GTSRB dataset in the directory layout supplied by the dataset provider.
The main notebook is configured for the Kaggle dataset
[`meowmeowmeowmeowmeow/gtsrb-german-traffic-sign`](https://www.kaggle.com/datasets/meowmeowmeowmeowmeow/gtsrb-german-traffic-sign).

On Kaggle:

1. Import `final_code-py.ipynb` as a notebook.
2. Add the GTSRB dataset to the notebook as an input.
3. Check the `ROOT` setting in the notebook's `CFG` configuration and update it if your dataset
   is mounted at a different path.
4. Run the notebook from the beginning. The setup cell installs PennyLane; if the environment
   requires a kernel restart after installation, restart and run the cells again.

For a local run, download GTSRB from its provider, extract it, and set `CFG["ROOT"]` (and, if
needed, `CFG["ROOT_FALLBACKS"]`) to the extracted dataset directory. Dataset access and any
provider-specific terms are separate from this repository; do not commit the dataset itself.

## Software

The notebooks use Python and the following packages:

- PennyLane
- PyTorch
- NumPy
- pandas
- Matplotlib
- Pillow
- scikit-learn
- SciPy

The main notebook also uses a hand-written PyTorch state-vector engine for the noiseless quantum
model. It includes checks comparing that implementation with a PennyLane QNode. No GPU is
required by the default configuration; the notebook selects CPU execution.

## Results and reproducibility

The notebooks contain training and evaluation code, and some include saved outputs from previous
runs. Results depend on the dataset version, selected classes, random seeds, software versions,
and runtime environment. Run the notebook to regenerate results rather than treating saved cell
outputs as a guarantee.

The 16×16 quantum model simulates a 13-qubit state vector and can be computationally demanding.
The notebooks include configuration options and checkpointing behavior; review the relevant
configuration cells before starting a long run.

## Repository contents and exclusions

The initial repository contains this README and the main 16×16 experiment notebook. Other
experimental notebooks, the review presentation, and the paper PDF are left out. The paper is a
published article; do not redistribute it without permission. The `.gitignore` also excludes
datasets, model checkpoints, generated outputs, and notebook/Python temporary files.

Before making the repository public, review notebook outputs and metadata for personal details,
local file paths, credentials, or other private data. Add an appropriate open-source license if
you want others to be able to reuse the code; no license is included in this project yet.

## Citation

If you build on this project, cite the source paper:

> Fan, S., Shi, Y., Guggemos, T., & Zhu, Q. “Hybrid Quantum-Classical Convolutional Neural Network
> Model for Image Classification.” *IEEE Transactions on Neural Networks and Learning Systems*,
> 35(12), 18145–18158, 2024.
