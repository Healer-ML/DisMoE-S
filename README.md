<div align="center">

# DisMoE

### Training Resources for DisMoE-C/S

<p>
  <img src="https://img.shields.io/badge/Python-3.8-34495e?style=flat-square" alt="Python 3.8">
  <img src="https://img.shields.io/badge/PyTorch-2.1.1%2BCUDA%2012.1-5b7c99?style=flat-square" alt="PyTorch 2.1.1 with CUDA 12.1">
  <img src="https://img.shields.io/badge/GPU-RTX%203090-8c6d62?style=flat-square" alt="RTX 3090">
</p>

</div>

---

## 1. Environment

The dependency specification is provided in [`requirement.txt`](requirement.txt). The recorded training configuration is:

| Component | Version / configuration |
| :--- | :--- |
| Operating system | Ubuntu 20.04.5 LTS |
| Conda environment | `yu` |
| Python | 3.8.0 |
| PyTorch | 2.1.1+cu121 |
| TorchVision | 0.16.1+cu121 |
| CUDA | 12.1 |
| NumPy | 1.24.4 |
| pandas | 2.0.3 |
| GPU | 2 × NVIDIA GeForce RTX 3090, 24 GB each |

```bash
conda activate yu
pip install -r requirement.txt
```

## 2. Datasets

The training interface contains handlers for the following micro-expression datasets:

| Dataset | Script identifier | Evaluation protocol |
| :--- | :--- | :--- |
| CASME II | `casme2` | Subject-independent LOSO |
| SAMM | `SAMM` | Subject-independent LOSO|
| SMIC | `SMIC` | Subject-independent LOSO |
| CAS(ME)<sup>3</sup> | `CASME3` | Subject-independent LOSO; configurable class setting |
| MEVIEW | `meview` | Subject-independent LOSO |

Dataset files and cropped face-frame directories are not included. They should be supplied locally through the `root_path` and `label_path` arguments used by the training interface.

## 3. Training Interface

The code namespace is consolidated under a single `DisMoE/` directory:

| File | Role |
| :--- | :--- |
| [`DisMoE/main.py`](DisMoE/main.py) | Training entry point |
| [`DisMoE/option.py`](DisMoE/option.py) | Command-line configuration |
| [`DisMoE/model.py`](DisMoE/model.py) | Model interface |
| [`DisMoE/train_epoch.py`](DisMoE/train_epoch.py) | Epoch-level training interface |
| [`DisMoE/data_me.py`](DisMoE/data_me.py) | Dataset loading interface |
| [`DisMoE/data_me2.py`](DisMoE/data_me2.py) | Alternative dataset loading interface |

Server-side launcher interfaces are kept at the repository root:

| Launcher | Purpose |
| :--- | :--- |
| [`train_samm.sh`](train_samm.sh) | SAMM training launcher |
| [`train_queue.sh`](train_queue.sh) | Multi-GPU training queue launcher |

Typical argument patterns used by the server launchers are:

```text
train_samm.sh --dataset SAMM --root_path <dataset_root> --label_path <annotation_file>
train_queue.sh <gpu_id> <class_count>
```

## 4. Model Architecture

<div align="center">
  <img src="assets/DisMoE_overview.png" alt="DisMoE model architecture" width="98%">
    <em>Overview of the DisMoE framework used by the training experiments.</em>
</div>

## 5. Repository Structure

```text
.
├── DisMoE/
│   ├── data_me.py
│   ├── data_me2.py
│   ├── main.py
│   ├── model.py
│   ├── option.py
│   └── train_epoch.py
├── assets/
│   └── DisMoE_overview.png
├── requirement.txt
├── train_queue.sh
├── train_samm.sh
└── README.md
```

## 6. Public Code Scope

The Python and shell files in this repository are structural placeholders without implementation code. The complete implementation and server-specific paths remain on the private training server.
