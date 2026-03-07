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

---

# Project Structure

### 1. pretrained_models/
Contains pretrained models trained on **synthetic** and **real-world** datasets.

### 2. Data/
Contains training and testing datasets.

### 3. Main_Model.py
Implements the **main model architecture**, which fuses **Deformable Convolutional Networks** and the **Deep Residual Channel Attention (DRCA) Network**.  
This file also reports the **total number of model parameters**.

### 4. Deformable.py
Implements the **Deformable Convolution layer** used for adaptive feature extraction.

### 5. DeformNet.py
Implements the **Spatial Feature Extraction (SPFE)** network for **depth-dependent LF view synthesis**.

### 6. MIDeform.py
Implements the **Angular Feature Extraction (AFE)** network for **non-depth-dependent LF view synthesis**.

### 7. RCB.py
Implements the **Deep Residual Channel Attention Network (DRCA)** including **Residual Channel Attention Blocks (RCABs)**.

### 8. Opt.py
Contains model configuration parameters and argument definitions.

### 9. Training_model.py
Script used for **training the model**.

### 10. Test_Model.py
Script used for **testing the pretrained model and generating results**.

---

# Running the Code

## Testing

```bash
python Test_Model.py
