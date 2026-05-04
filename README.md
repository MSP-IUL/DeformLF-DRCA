# Dual Representation-based Light Field View Synthesis using Deformable Convolutional and Deep Residual Channel Attention Networks

## Abstract
Light Field (LF) cameras simultaneously capture both intensity values and directional information of light rays in a single exposure, providing a unique perspective for computational photography and 3D geometry perception. However, existing LF cameras are constrained by sensor resolution, limiting their ability to capture high spatial and angular resolutions simultaneously. 

To mitigate these issues, various learning-based methods have been proposed to increase the angular resolution of captured LFs, known as **Light Field View Synthesis (LFVS)**. Many of these methods either neglect essential geometric cues or rely on neural networks with large receptive fields, which restrict their ability to accurately exploit LF structural characteristics.

To address these challenges, this paper introduces a **dual representation-based LFVS method** that employs **Deformable Convolutional Networks** and **Deep Residual Channel Attention (DRCA) Networks**.

The proposed method includes two main modules:

1. **Coarse Light Field View Synthesis (CLFVS)** for initial LF view synthesis.
2. **Coarse-To-Fine Refinement (CFR)** for final quality enhancement.

The **CLFVS module** relies on deformable convolutions to adaptively extract LF features using two parallel networks:

- **Spatial Feature Extraction (SPFE)** – depth-dependent LFVS approach.
- **Angular Feature Extraction (AFE)** – non-depth-dependent LFVS approach.

The **CFR module** refines the CLFVS output using a **DRCA network**, which employs dense residual connections between residual groups instead of conventional convolutional layers. The DRCA network uses **Residual Channel Attention Blocks (RCABs)** to model inter-channel dependencies, selectively enhancing meaningful features while suppressing irrelevant ones.

The proposed method achieves strong performance on both **synthetic and real-world LF benchmarks**.

## Project Structure
## Model Selection
To toggle between the **Synthetic** and **Real-World** models:
* **Modify the `MODEL_NAME` variable** within the `run.sh` script.
* **Note:** The environment defaults to the `synthetic_model` if no changes are made.

## Dataset Evaluation
To perform evaluations on various datasets:
* **Update the dataset identifiers** in `opt.py`.
* **Verify Data Paths:** Ensure the corresponding data is present in the `/Data/[dataset_name]` directory.

---


| Folder / File | Description |
|---------------|-------------|
| `pretrained_models/` | Pretrained LFVS models (synthetic and Real). |
| `Data/` | Snythetic  and real-world datasets. |
| `Main_Model.py` | Main model architecture combining deformable conv + DRCA. Reports model parameters. |
| `Deformable.py` | Deformable convolution layer for adaptive feature extraction. |
| `DeformNet.py` | SPFE network (depth-dependent LFVS). |
| `MIDeform.py` | AFE network (non-depth-dependent LFVS). |
| `RCB.py` | DRCA network with Residual Channel Attention Blocks. |
| `Opt.py` | Model configuration parameters and argument definitions. |
| `Training_model.py` | Training script for LFVS model. |
| `Test_Model.py` | Testing script for generating synthesized views and quantitative results. |

## 1. Model Parameters and Inference Time

The total number of model parameters is reported automatically during the inference phase of the `synthetic_model`.
Inference time is explicitly not reported due to inherent hardware disparities between local and cloud environments.

## 2. Testing Pretrained Models

Run the LFVS test script:

```bash
python Test_Model.py 
```

### Outputs
All persistent outputs are directed to the `/results` directory. Output files are organized by the specific `run_test_name` and its associated unique ID.

* **`quant_results/`**: Contains quantitative evaluation files reporting **PSNR** and **SSIM** metrics for each tested Light Field Image (LFI).
* **`SaveImg/`**: Stores all synthesized Light Field views generated during the inference process.

## 3. For Retraining  
Run the follow code
```bash
python Train_Model.py 
```

## 4. Angular Consistency
 Change the run file configuration (as mentioned in run file for angular consistency) for angular consistency and then run that will generate anagular consistency output . 
## 5. Reproducibility Notes
 Keep batch size, patch size, and checkpoint paths consistent for reproducible metrics.

> ### ⚠️ Note on Reproducibility and Performance
> 
> **Numerical Deviations:** Results may exhibit marginal deviations from previously published values due to **stochastic hardware behavior**, including GPU non-determinism, floating-point precision variance across architectures, and hardware-specific CUDA kernel optimizations. 
>
> **Patch-Based Inference:** To ensure execution stability across diverse hardware profiles and to mitigate **Out-of-Memory (OOM)** constraints, the inference pipeline has been optimized to perform **patch-based analysis**. 
>
> While these modifications ensure cross-platform compatibility, the resulting latency profiles and quantitative metrics (PSNR/SSIM) may vary slightly from benchmarks generated on high-memory, centralized clusters. These variations are expected and inherent to the transition between different high-performance computing environments.
