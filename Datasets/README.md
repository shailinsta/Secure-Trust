# SecureTrust-FL Dataset

This directory contains the datasets used for training and evaluating the SecureTrust-FL framework.

## Download Dataset

The complete dataset package can be downloaded from Hugging Face:

https://huggingface.co/datasets/ShamsTahzib/Secure_Trust_FT

## Installation

1. Download the dataset ZIP file from Hugging Face.
2. Place the ZIP file inside this `data/` directory.

The directory structure should look like:

```
data/
├── CICIDS2017.csv
├── UNSW_NB15.csv
├── BoT_IoT.csv
└── README.md
```

If you prefer to keep the compressed file:

```
data/
├── Secure_Trust_FT.zip
└── README.md
```

## Dataset Description

The SecureTrust-FL framework uses three widely adopted intrusion detection datasets:

### CICIDS2017
- Modern enterprise network intrusion dataset.
- Contains benign and attack traffic.
- Includes brute force, DDoS, botnet, and web attacks.

### UNSW-NB15
- Contemporary network security dataset.
- Contains normal and malicious traffic records.
- Covers multiple attack categories including exploits, reconnaissance, and worms.

### BoT-IoT
- IoT-focused cybersecurity dataset.
- Includes botnet and distributed attack traffic.
- Designed for evaluating intrusion detection in IoT environments.

## Preprocessing

Before federated training, the datasets undergo:

- Feature harmonization
- Missing value handling
- Label normalization
- Standard scaling
- Binary attack classification
- Mutual information feature selection

The final federated dataset uses a common feature space consisting of 13 selected features.

## Federated Client Mapping

| Client | Dataset |
|----------|----------|
| Client 1 | CICIDS2017 |
| Client 2 | UNSW-NB15 |
| Client 3 | BoT-IoT |

Each dataset acts as an independent federated client to simulate heterogeneous and non-IID environments.


## Citation

If you use this dataset in your research, please cite:

Hugging Face Dataset Repository:
https://huggingface.co/datasets/ShamsTahzib/Secure_Trust_FT
```