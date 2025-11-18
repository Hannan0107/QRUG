# QRUG — Quantum Machine Learning for Targeted Drug Discovery

QRUG is a quantum–enhanced machine learning project designed to predict **pIC50**
values of compounds targeting **Human Acetylcholinesterase (CHEMBL220)**.
The project integrates **cheminformatics**, **classical machine learning**, and
**quantum computing** using **Qulacs** to explore how quantum kernels can improve
bioactivity prediction.

This repository contains the complete pipeline:  
data retrieval → preprocessing → descriptor generation → analysis → quantum kernel → regression model.

<img width="777" height="440" alt="image" src="https://github.com/user-attachments/assets/7b9500a4-f392-47fe-a28d-6a3cabe7640b" />


---

## 🚀 Project Goals

- Build a **quantum-enhanced Support Vector Regression (QSVR)** model using Qulacs.
- Retrieve real bioactivity data from **ChEMBL** and convert IC50 → pIC50.
- Generate **PubChem fingerprints** using PaDEL-Descriptor.
- Perform **exploratory data analysis** (EDA) using RDKit descriptors.
- Train and evaluate a quantum kernel–based model for drug potency prediction.
- Provide a scalable framework for future quantum drug-discovery research.

---

## 🧬 Workflow Overview

### **1️⃣ Data Collection (ChEMBL API)**
- Retrieve bioactivity data for CHEMBL220.
- Extract:  
  - `canonical_smiles`  
  - IC50 values  
  - molecule identifiers  

### **2️⃣ Preprocessing**
- Remove missing values and duplicate SMILES.
- Convert IC50 → pIC50 using:  
  $pIC_{50} = -\log_{10}(IC_{50} \times 10^{-9})$

- Classify bioactivity:
  - Active: IC50 ≤ 1000 nM  
  - Inactive: IC50 ≥ 10000 nM  
  - Intermediate removed for clean learning

### **3️⃣ Exploratory Data Analysis**
Using RDKit:
- Lipinski descriptors:
  - Molecular Weight
  - LogP
  - Hydrogen bond donors/acceptors
- Chemical space plots  
- Mann–Whitney U statistical comparison  
- Insights:
  - pIC50 separates classes  
  - Lipinski descriptors **do NOT** significantly differentiate active vs inactive  
  - Justifies use of quantum feature mappings

### **4️⃣ Descriptor Generation**
Using PaDEL-Descriptor:
- Generate **881-bit PubChem fingerprints**
- Final dataset = 881 features + pIC50 target

### **5️⃣ Quantum Kernel Construction**
Using **Qulacs**:
- Build a 10-qubit quantum feature map  
- Apply RX + RZ rotations parameterized by molecular fingerprints  
- Introduce entanglement via a chain of CNOT gates  
- Compute quantum kernel:  
  $K(x_i, x_j) = |\langle \psi(x_i) \mid \psi(x_j) \rangle|^2$


### **6️⃣ Regression Model**
- Train **SVR with precomputed quantum kernel**
- Evaluate using:
  - R² Score  
  - MSE  
- Compare with classical SVR baseline
  
---
# DFD (0-Level)
<img width="770" height="1255" alt="image" src="https://github.com/user-attachments/assets/fa95f18d-c7ce-45c8-b248-d8ec97061bea" />


