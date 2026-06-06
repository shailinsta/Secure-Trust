# SecureTrust-FL: Trust-Aware Privacy-Preserving Federated Learning for Network Intrusion Detection


The proliferation of distributed network environments and the Internet of Things (IoT) has increased the need for privacy-preserving intrusion detection systems capable of operating effectively under heterogeneous and non-independent and identically distributed (non-IID) data conditions. This paper proposes SecureTrust-FL, a trust-aware federated learning framework for privacy-preserving intrusion detection. The framework integrates Federated Learning, Blockchain-based Trust Management, Differential Privacy, FGSM-based Adversarial Learning, and Zero-Trust Security principles to support secure collaborative learning without requiring raw data sharing among participating entities. The framework is evaluated using three benchmark intrusion detection datasets, namely CICIDS2017, UNSW-NB15, and BoT-IoT, which are treated as independent federated clients. Experimental results demonstrate that the proposed framework achieves an overall Accuracy of 92.58%, Balanced Accuracy of 92.56%, F1-Score of 92.53%, and AUC of 96.83% across heterogeneous datasets. The results indicate that the federated model can effectively learn from distributed and heterogeneous data while preserving data privacy.Further analysis reveals the impact of class imbalance on intrusion detection performance, particularly in datasets containing skewed attack distributions, highlighting the importance of Balanced Accuracy and F1-Score in addition to overall Accuracy. Differential privacy experiments demonstrate the privacy–utility trade-off, where stronger privacy protection leads to a reduction in model performance. Adversarial robustness evaluation using FGSM perturbations also shows a noticeable decline in detection performance, indicating the need for stronger defense mechanisms against adversarial attacks. In addition, the trust ledger enhances transparency and accountability by monitoring client participation and maintaining trust records throughout the collaborative learning process. The results demonstrate that SecureTrust-FL provides an effective framework for privacy-preserving collaborative intrusion detection while integrating trust management, privacy protection, and secure federated learning within a unified architecture.


SecureTrust-FL integrates:

- Federated Learning (FL)
- Trust Ledger Monitoring
- Differential Privacy (DP)
- FGSM-based Adversarial Robustness Evaluation
- FedProx Regularization
- Mixup Data Augmentation
- Zero-Trust Security Principles

The framework is evaluated using three benchmark intrusion detection datasets: CICIDS2017, UNSW-NB15, and BoT-IoT, which are treated as independent federated clients to simulate realistic non-IID environments.

---

## Key Features

### Privacy-Preserving Federated Learning
- Collaborative model training without raw data sharing
- Distributed client-server architecture
- Support for heterogeneous and non-IID datasets

### Trust Ledger Monitoring
- Tracks client participation throughout federated training
- Records trust scores, validation performance, and update statistics
- Provides transparency and auditability
- Monitoring-only mechanism that does not affect FedAvg aggregation

### Differential Privacy Evaluation
- Gradient clipping
- Gaussian noise injection
- Privacy-utility trade-off analysis

### Adversarial Robustness Assessment
- Fast Gradient Sign Method (FGSM) attack evaluation
- Robustness testing under multiple perturbation strengths

### Data Imbalance Handling
- Feature harmonization across datasets
- Standardized preprocessing pipeline
- Balanced evaluation using multiple metrics

---

## System Architecture

```text
                    ┌──────────────────────┐
                    │ Federated Server     │
                    │      (FedAvg)        │
                    └──────────┬───────────┘
                               │
          ┌────────────────────┼────────────────────┐
          │                    │                    │
          ▼                    ▼                    ▼

     Client 1             Client 2            Client 3
   CICIDS2017           UNSW-NB15            BoT-IoT

          │                    │                    │
          ▼                    ▼                    ▼

     Local MLP           Local MLP          Local MLP
     Training            Training           Training

          └─────────────────────────────────────────┘
                               │
                               ▼

                  Global Model Aggregation

                               │
                               ▼

                  Trust Ledger Monitoring
```

---

## Datasets

The framework uses three publicly available intrusion detection datasets:

| Dataset | Description |
|----------|-------------|
| CICIDS2017 | Modern network intrusion dataset containing diverse attack scenarios |
| UNSW-NB15 | Realistic network traffic with contemporary attack categories |
| BoT-IoT | IoT-focused intrusion detection dataset containing botnet attacks |

---

## Federated Client Dataset Configuration

| Client | Dataset | Training Samples | Test Samples | Attack Distribution | Feature Dimension |
|----------|----------|----------------:|-------------:|---------------------|------------------:|
| Client 1 | CICIDS2017 | 7,225 | 1,500 | Moderately Balanced | 13 |
| Client 2 | UNSW-NB15 | 1,806 | 375 | Highly Imbalanced | 13 |
| Client 3 | BoT-IoT | 7,078 | 1,470 | Attack-Dominant | 13 |

The datasets were harmonized into a common feature space using mutual information-based feature selection and preprocessing techniques.

---

## Training Configuration

| Parameter | Value |
|------------|---------|
| Communication Rounds | 20 |
| Local Epochs | 8 |
| Batch Size | 128 |
| Learning Rate | 0.001 |
| Clients per Round | 3 |
| FedProx μ | 0.01 |
| Input Features | 13 |
| FGSM ε | {0.000, 0.005, 0.010, 0.050, 0.100, 0.200} |
| Differential Privacy Noise (σ) | {0.000, 0.001, 0.005, 0.010} |

---

## Model Architecture

Each client trains a lightweight Multi-Layer Perceptron (MLP):

```
Input Layer (13 Features)
        │
        ▼
Fully Connected Layer
        │
       ReLU
        │
        ▼
Fully Connected Layer
        │
       ReLU
        │
        ▼
Output Layer
(Binary Classification)
```

Classification Labels:

- 0 → Benign Traffic
- 1 → Malicious Traffic

---

## Experimental Results

### Global Performance

| Metric | Score (%) |
|----------|----------:|
| Accuracy | 92.58 |
| Balanced Accuracy | 92.56 |
| Micro F1-Score | 92.53 |
| AUC | 96.83 |

These results demonstrate the ability of SecureTrust-FL to effectively learn from distributed and heterogeneous intrusion detection datasets while preserving privacy.

---

### Dataset-wise Performance

| Dataset | Accuracy (%) | Balanced Accuracy (%) | Weighted F1 (%) |
|----------|------------:|---------------------:|---------------:|
| CICIDS2017 | 93.93 | 95.21 | 94.60 |
| UNSW-NB15 | 72.80 | 74.13 | 73.17 |
| BoT-IoT | 96.26 | 96.26 | 98.09 |

The results indicate strong generalization across heterogeneous network environments.

---

## Differential Privacy Evaluation

The framework evaluates privacy preservation by injecting Gaussian noise into model updates.

Noise levels tested:

```
σ = 0.000
σ = 0.001
σ = 0.005
σ = 0.010
```

Results demonstrate the expected privacy–utility trade-off, where stronger privacy guarantees slightly reduce detection performance while maintaining acceptable accuracy.

---

## Adversarial Robustness Evaluation

FGSM adversarial attacks were used to assess robustness.

Attack strengths tested:

```
ε = 0.000
ε = 0.005
ε = 0.010
ε = 0.050
ε = 0.100
ε = 0.200
```

The framework maintains strong performance under low perturbation levels while showing degradation under stronger adversarial attacks, highlighting future opportunities for adversarial defense integration.

---

## Trust Ledger Monitoring

SecureTrust-FL incorporates a trust ledger that records:

- Client participation history
- Validation accuracy
- Reliability metrics
- Trust scores
- Model update statistics
- Communication round information

The trust ledger improves transparency and auditability while remaining independent of the FedAvg aggregation process.

---

## Evaluation Metrics

The framework reports:

- Accuracy
- Balanced Accuracy
- Precision
- Recall
- F1-Score
- ROC-AUC
- Confusion Matrix
- Average Precision (AP)

---

## Requirements

```bash
Python >= 3.10
PyTorch
Flower
NumPy
Pandas
Scikit-learn
Matplotlib
Seaborn
```

Install dependencies:

```bash
pip install torch flwr numpy pandas scikit-learn matplotlib seaborn
```

---

## Running the Project

execute the notebook:

```bash
jupyter notebook Secure_Trust.ipynb
```

---

## Project Structure

```text
SecureTrust-FL/
│
├── Secure_Trust.ipynb
├── datasets/
│   ├── CICIDS2017/
│   ├── UNSW-NB15/
│   └── BoT-IoT/
│
├── results/
│   ├── global_metrics.csv
│   ├── trust_scores.csv
│   ├── fgsm_results.csv
│   ├── dp_results.csv
│   └── confusion_matrix.png
│
├── figures/
├── requirements.txt
└── README.md
```

---

## Research Contributions

- Privacy-preserving federated intrusion detection framework.
- Cross-dataset evaluation using CICIDS2017, UNSW-NB15, and BoT-IoT.
- Trust-ledger-based monitoring for transparency and auditability.
- Differential privacy evaluation in federated IDS.
- FGSM-based adversarial robustness analysis.
- Comprehensive study of heterogeneous non-IID federated learning environments.

---


## License

This project is intended for academic and research purposes.
