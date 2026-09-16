<div align="center">

# DisMoE-C-S

### Training Environment, Datasets, and Launchers

<p>
  <img src="https://img.shields.io/badge/Python-3.8-34495e?style=flat-square" alt="Python 3.8">
  <img src="https://img.shields.io/badge/PyTorch-2.1.1%2BCUDA%2012.1-5b7c99?style=flat-square" alt="PyTorch 2.1.1 with CUDA 12.1">
  <img src="https://img.shields.io/badge/GPU-RTX%203090-8c6d62?style=flat-square" alt="RTX 3090">
</p>

</div>

---

## Environment

The following configuration is recorded from the training server:

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

Example environment activation:

```bash
conda activate yu
python --version
```

## Datasets

The training entry points currently support the following datasets:

| Dataset | Identifier used by the scripts | Annotation / split |
| :--- | :--- | :--- |
| CASME II | `casme2` | Subject-independent LOSO |
| SAMM | `SAMM` | Subject-independent LOSO; 3- or 5-class setting |
| SMIC | `SMIC` | Subject-independent LOSO |
| CAS(ME)<sup>3</sup> | `CASME3` | Subject-independent LOSO; configurable class setting |
| MEVIEW | `meview` | Subject-independent LOSO |
| DFME | `DFME` | Predefined training / validation split |

Dataset files and face-frame directories should be prepared locally and passed through the corresponding `root_path` and `label_path` arguments. No dataset files are included in this repository.

## Training Entry Points

The public repository keeps the Python file layout while omitting the implementation contents. The following files correspond to the training entry points used on the server:

| File | Role |
| :--- | :--- |
| `scripts/Ad-TMM/main.py` | Main training entry point for the current experiment branch |
| `scripts/Ad-TMM/option.py` | Command-line arguments and training configuration |
| `scripts/Ad-TMM/train_epoch.py` | Epoch-level training and validation interface |
| `scripts/Ad-TMM/data_me.py` | Dataset loading interface |
| `scripts/Ad-TMM/data_me2.py` | Alternative dataset loading interface |
| `scripts/DisMoE/main.py` | Main training entry point for the DisMoE branch |
| `scripts/DisMoE/option.py` | DisMoE training arguments |
| `scripts/DisMoE/train_epoch.py` | DisMoE epoch-level training interface |
| `scripts/TMM-ab/main.py` | Ablation experiment entry point |
| `scripts/TMM-ab/option.py` | Ablation experiment arguments |
| `scripts/TMM-ab/train_epoch.py` | Ablation training interface |
| `scripts/me-MoE_cas3/main.py` | CAS(ME)<sup>3</sup> experiment entry point |
| `scripts/me-MoE_cas3/option.py` | CAS(ME)<sup>3</sup> experiment arguments |
| `scripts/me-MoE_cas3/train_epoch.py` | CAS(ME)<sup>3</sup> training interface |

## Server Launchers

The following launchers were used for server-side experiments:

| Launcher | Purpose |
| :--- | :--- |
| `scripts/retrain7.sh` | Repeated SAMM retraining over fusion settings and seeds |
| `scripts/run_samm_full_gpu_queue.sh` | Multi-GPU SAMM training queue for 3- or 5-class experiments |
| `scripts/queue_240.sh` | Queued ablation runs with GPU assignment and output tracking |

Typical launcher arguments are:

```text
retrain7.sh <fusion_method> <seed> <output_directory>
run_samm_full_gpu_queue.sh <gpu_id> <class_count>
queue_240.sh <gpu_id> <wait_name> <run_spec> ...
```

## Public Snapshot

The `.py` files in `scripts/` are intentionally empty placeholders. The implementation remains on the private training server and is not included in this public snapshot.
