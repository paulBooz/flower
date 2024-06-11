---
title: StatAvg - Mitigating Data Heterogeneity in Federated Learning for Intrusion Detection Systems
url: https://arxiv.org/abs/2405.13062
labels: [label1, label2] # please add between 4 and 10 single-word (maybe two-words) labels (e.g. system heterogeneity, image classification, asynchronous, weight sharing, cross-silo). Do not use ""
dataset: [TON_IoT] # list of datasets you include in your baseline. Do not use ""
---

# StatAvg: Mitigating Data Heterogeneity in Federated Learning for Intrusion Detection Systems


**Paper:** https://arxiv.org/abs/2405.13062

**Authors:** Pavlos S. Bouzinis, Panagiotis Radoglou-Grammatikis, Ioannis Makris, Thomas Lagkas, Vasileios Argyriou, Georgios Th. Papadopoulos, Panagiotis Sarigiannidis, George K. Karagiannidis

**Abstract:** Federated learning (FL) is a decentralized learning technique that enables participating devices to collaboratively build a shared Machine Leaning (ML) or Deep Learning (DL) model without revealing their raw data to a third party. Due to its privacy-preserving nature, FL has sparked widespread attention for building Intrusion Detection Systems (IDS) within the realm of cybersecurity. However, the data heterogeneity across participating domains and entities presents significant challenges for the reliable implementation of an FL-based IDS. In this paper, we propose an effective method called Statistical Averaging (StatAvg) to alleviate non-independently and identically (non-iid) distributed features across local clients' data in FL. In particular, StatAvg allows the FL clients to share their individual data statistics with the server, which then aggregates this information to produce global statistics. The latter are shared with the clients and used for universal data normalisation. It is worth mentioning that StatAvg can seamlessly integrate with any FL aggregation strategy, as it occurs before the actual FL training process. The proposed method is evaluated against baseline approaches using datasets for network and host Artificial Intelligence (AI)-powered IDS. The experimental results demonstrate the efficiency of StatAvg in mitigating non-iid feature distributions across the FL clients compared to the baseline methods.


## About this baseline

**What’s implemented:** The code in this directory replicates the experiments in the above paper for TON IoT datasets, which proposed the StatAvg algorithm. It replicates the Figure 3 of the paper.

**Datasets:** TON IoT dataset (linux memory logs)

**Hardware Setup:**  These experiments were run on a desktop machine with 16 CPU threads. Any machine with 4 CPU cores or more would be able to run it in a reasonable amount of time

**Contributors:** TBD


## Experimental Setup

**Task:** :warning: *_what’s the primary task that is being federated? (e.g. image classification, next-word prediction). If you have experiments for several, please list them_*

**Model:** :warning: *_provide details about the model you used in your experiments (if more than use a list). If your model is small, describing it as a table would be :100:. Some FL methods do not use an off-the-shelve model (e.g. ResNet18) instead they create your own. If this is your case, please provide a summary here and give pointers to where in the paper (e.g. Appendix B.4) is detailed._*

**Dataset:** :warning: *_Earlier you listed already the datasets that your baseline uses. Now you should include a breakdown of the details about each of them. Please include information about: how the dataset is partitioned (e.g. LDA with alpha 0.1 as default and all clients have the same number of training examples; or each client gets assigned a different number of samples following a power-law distribution with each client only instances of 2 classes)? if  your dataset is naturally partitioned just state “naturally partitioned”; how many partitions there are (i.e. how many clients)? Please include this an all information relevant about the dataset and its partitioning into a table._*

**Training Hyperparameters:** :warning: *_Include a table with all the main hyperparameters in your baseline. Please show them with their default value._*


## Environment Setup

:warning: _The Python environment for all baselines should follow these guidelines in the `EXTENDED_README`. Specify the steps to create and activate your environment. If there are any external system-wide requirements, please include instructions for them too. These instructions should be comprehensive enough so anyone can run them (if non standard, describe them step-by-step)._


## Running the Experiments

:warning: _Provide instructions on the steps to follow to run all the experiments._
```bash  
# The main experiment implemented in your baseline using default hyperparameters (that should be setup in the Hydra configs) should run (including dataset download and necessary partitioning) by executing the command:

poetry run python -m <baseline-name>.main <no additional arguments> # where <baseline-name> is the name of this directory and that of the only sub-directory in this directory (i.e. where all your source code is)

# If you are using a dataset that requires a complicated download (i.e. not using one natively supported by TF/PyTorch) + preprocessing logic, you might want to tell people to run one script first that will do all that. Please ensure the download + preprocessing can be configured to suit (at least!) a different download directory (and use as default the current directory). The expected command to run to do this is:

poetry run python -m <baseline-name>.dataset_preparation <optional arguments, but default should always run>

# It is expected that you baseline supports more than one dataset and different FL settings (e.g. different number of clients, dataset partitioning methods, etc). Please provide a list of commands showing how these experiments are run. Include also a short explanation of what each one does. Here it is expected you'll be using the Hydra syntax to override the default config.

poetry run python -m <baseline-name>.main  <override_some_hyperparameters>
.
.
.
poetry run python -m <baseline-name>.main  <override_some_hyperparameters>
```


## Expected Results

:warning: _Your baseline implementation should replicate several of the experiments in the original paper. Please include here the exact command(s) needed to run each of those experiments followed by a figure (e.g. a line plot) or table showing the results you obtained when you ran the code. Below is an example of how you can present this. Please add command followed by results for all your experiments._

```bash
# it is likely that for one experiment you need to sweep over different hyperparameters. You are encouraged to use Hydra's multirun functionality for this. This is an example of how you could achieve this for some typical FL hyperparameteres

poetry run python -m <baseline-name>.main --multirun num_client_per_round=5,10,50 dataset=femnist,cifar10
# the above command will run a total of 6 individual experiments (because 3client_configs x 2datasets = 6 -- you can think of it as a grid).

[Now show a figure/table displaying the results of the above command]

# add more commands + plots for additional experiments.
```
