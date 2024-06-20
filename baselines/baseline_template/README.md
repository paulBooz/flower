---
title: StatAvg - Mitigating Data Heterogeneity in Federated Learning for Intrusion Detection Systems
url: https://arxiv.org/abs/2405.13062
labels: [intrusion detection system, non-iid data, statistical averaging] # please add between 4 and 10 single-word (maybe two-words) labels (e.g. system heterogeneity, image classification, asynchronous, weight sharing, cross-silo). Do not use ""
dataset: [TON_IoT] # list of datasets you include in your baseline. Do not use ""
---

# StatAvg: Mitigating Data Heterogeneity in Federated Learning for Intrusion Detection Systems


**Paper:** https://arxiv.org/abs/2405.13062

**Authors:** Pavlos S. Bouzinis, Panagiotis Radoglou-Grammatikis, Ioannis Makris, Thomas Lagkas, Vasileios Argyriou, Georgios Th. Papadopoulos, Panagiotis Sarigiannidis, George K. Karagiannidis

**Abstract:** Federated learning (FL) is a decentralized learning technique that enables participating devices to collaboratively build a shared Machine Leaning (ML) or Deep Learning (DL) model without revealing their raw data to a third party. Due to its privacy-preserving nature, FL has sparked widespread attention for building Intrusion Detection Systems (IDS) within the realm of cybersecurity. However, the data heterogeneity across participating domains and entities presents significant challenges for the reliable implementation of an FL-based IDS. In this paper, we propose an effective method called Statistical Averaging (StatAvg) to alleviate non-independently and identically (non-iid) distributed features across local clients' data in FL. In particular, StatAvg allows the FL clients to share their individual data statistics with the server, which then aggregates this information to produce global statistics. The latter are shared with the clients and used for universal data normalisation. It is worth mentioning that StatAvg can seamlessly integrate with any FL aggregation strategy, as it occurs before the actual FL training process. The proposed method is evaluated against baseline approaches using datasets for network and host Artificial Intelligence (AI)-powered IDS. The experimental results demonstrate the efficiency of StatAvg in mitigating non-iid feature distributions across the FL clients compared to the baseline methods.


## About this baseline

**What’s implemented:** The code in this directory replicates the experiments in the above paper for TON IoT datasets, which proposed the StatAvg algorithm. It replicates the Figure 3 of the paper.

**Datasets:** TON IoT dataset (linux memory logs). Online at https://research.unsw.edu.au/projects/toniot-datasets

**Hardware Setup:**  These experiments were run on a desktop machine with 16 CPU threads. Any machine with 4 CPU cores or more would be able to run it in a reasonable amount of time.

**Contributors:** TBD


## Experimental Setup

**Task:** Classification of cyberattacks

**Model:** A simple MLP with three hidden layers.

**Dataset:** This baseline only includes the TON IoT dataset. By default, it will be partitioned into 5 clients following a stratified split based on the labels. The settings are as follows:
| Dataset | #classes | #partitions | partitioning method | partition settings |
| :------ | :---: | :---: | :---: | :---: |
| TON IoT | 6 | 5 | stratified based on labels | 6 classes per client |

**Training Hyperparameters:** The following table shows the main hyperparameters for this baseline with their default value
| Description | Default Value |
| ----------- | ----- |
| total clients | 5 |
| clients per round | 5 |
| number of rounds | 50 |
| local epochs | 2 |
| client resources | {'num_cpus': 3.0, 'num_gpus': 0.0 }|
| data partition | stratified based on labels (6 classes per client) |
| optimizer | Adam |


## Environment Setup

To construct the Python environment, simply run:

```bash
# Set directory to use python 3.10 (install with `pyenv install <version>` if you don't have it)
pyenv local 3.10.13

# Tell poetry to use python3.10
poetry env use 3.10.13

# Install
poetry install
```

## Running the Experiments

To run StatAvg with TON IoT baseline, first ensure you have activated your Poetry environment (execute `poetry shell` from this directory), then:

```bash
python -m statavg.main # this will run using the default settings in the `conf/base.yaml`

# you can override settings directly from the command line
python -m statavg.main num_rounds=20 # will set number of rounds to 20
```

## Expected Results

To reproduce the results of the paper (Fig. 3., StatAvg), simply run:

```bash
python -m statavg.main   # default settings
```

In the paper, server-side evaluation is not implemented, as it is considered that the server does not own any data. However, one can enable server-side evaluation by executing:

```bash
# enable server-side evaluation with the data ratio of your preference. Default settings do not include this option.
python -m statavg.main include_testset.flag=true include_testset.ratio=0.15
```
