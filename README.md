
# Predicting Missing Brain Connectivity Values

---

## Overview
This project focuses on **predicting missing values** in brain connectivity matrices using **EdgeConv-based Graph Neural Networks (EGNNs)**.

We simulate missing edges across EEG-based brain networks, normalize per frequency band, apply random multi-level masking, and train a model to accurately restore the hidden connections.

The final model achieves strong predictive performance across six major EEG frequency bands.

---

## Pipeline Summary
- **Input**:  
  Connectivity matrices of shape **[6 bands × 68 regions × 68 regions]** (Desikan-Killiany Atlas).
- **Normalization**:  
  Each frequency band is normalized separately for each patient.
- **Masking**:  
  Random masking of **10–60 edges** (including self-loops) per graph.
- **Augmentation**:  
  Noise injection during training for robustness.
- **Model**:  
  **EdgeConv** GNN to predict missing edges from node and edge features.
- **Evaluation**:  
  Correlation plots, scatter plots, heatmaps for predicted vs true edges.

---


## Methods

- **Graph Construction**:  
  Each patient's connectivity matrix is converted into a graph, with nodes (brain regions) and masked edge features.
  
- **Model**:  
  - Node encoder: simple MLP
  - Edge encoder: simple MLP
  - EdgeConv aggregation (2 layers)
  - Edge regression head
  
- **Loss**:  
  Weighted MSE loss computed only on masked edges.

- **Training Details**:  
  - Optimizer: Adam
  - Learning Rate Scheduler: ReduceLROnPlateau
  - Batch Size: 8
  - Early Stopping Patience: 50 epochs

---


## Requirements

- Python 3.8+
- PyTorch
- PyTorch-Geometric
- NumPy
- Matplotlib
- Pandas
- Scikit-Learn (optional for evaluation)

You can install dependencies with:
```bash
pip install -r requirements.txt
```


## Acknowledgements
- Brain region definitions based on the **Desikan-Killiany atlas**.
- Connectivity matrices simulated from EEG-based frequency bands.




