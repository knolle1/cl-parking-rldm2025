# Continual Reinforcement Learning for Cyber-Physical Systems: Lessons Learned and Open Challenges

This repository contains the code to reported in the extended abstract and the results presented at the poster session of RLDM 2025.

Parking environment adapted from [HighwayEnv](https://github.com/eleurent/highway-env) (date accessed: 12/05/2024)

PPO implementation adapted from implementation by [Wenlong Wang](https://github.com/realwenlongwang/PPO-Single-File-Notebook-Implementation) (date accessed: 25/06/2024)

## Abstract

Continual learning (CL) is a branch of machine learning that aims to enable agents to adapt and generalise previously
learned abilities so that these can be reapplied to new tasks or environments. This is particularly useful in multi-task
settings or in non-stationary environments, where the dynamics can change over time. This is particularly relevant in
cyber-physical systems such as autonomous driving. However, despite recent advances in CL, successfully applying it
to reinforcement learning (RL) is still an open problem.

This paper highlights open challenges in continual RL (CRL) based on experiments in an autonomous driving environment.
In this environment, the agent must learn to successfully park in four different scenarios corresponding to parking
spaces oriented at varying angles. The agent is successively trained in these four scenarios one after another, representing
a CL environment, using Proximal Policy Optimisation (PPO). These experiments exposed a number of open challenges
in CRL: finding suitable abstractions of the environment, oversensitivity to hyperparameters, catastrophic forgetting,
and efficient use of neural network capacity.

Based on these identified challenges, we present open research questions that are important to be addressed for creating
robust CRL systems. In addition, the identified challenges call into question the suitability of neural networks for CL.
We also identify the need for interdisciplinary research, in particular between computer science and neuroscience.

## Dependencies

1. Create and activate virtual environment:
	- With conda:
		- `conda create -n cl-parking python=3.10`
		- `conda activate cl-parking`
	- Alternatively with venv:
		- `python -m venv .venv`
		- `source .venv/bin/activate`
2. Install dependencies: `pip install -r requirements.txt`
3. Install ImageMagick (for generating videos): `conda install conda-forge::imagemagick==7.1.1_28`

## Running Experiments

1. Create configuration JSON file
2. Run `python train_eval.py --config PATH_TO_CONFIG`

To reproduce the results reported in the extended abstract and the results presented at the poster session of RLDM 2025, please run the following commands:

Run experiment with PPO agent trained sequentially in all four parking scenarios:
```
python train_eval.py --config ./config/baseline/sequential_in-order.json
```

Run experiment with PPO+EWC agent trained sequentially in all four parking scenarios:
```
python train_eval.py --config ./config/ppo-ewc/sequential_in-order.json
```

Run experiment to calculate EWC importances of PPO agent trained on single scenario:
```
python train_eval.py --config ./config/ppo-ewc/single_vertical.json
python train_eval.py --config ./config/ppo-ewc/single_diagonal-25.json
python train_eval.py --config ./config/ppo-ewc/single_diagonal-50.json
python train_eval.py --config ./config/ppo-ewc/single_parallel.json
```

Run experiments to test different configurations for parallel parking:
```
python train_eval.py --config ./config/baseline/single_parallel.json
python train_eval.py --config ./config/parallel-tuning/single_parallel_adj-head_xy-reward-switched.json
python train_eval.py --config ./config/parallel-tuning/single_parallel_adj-2M.json
python train_eval.py --config ./config/parallel-tuning/single_parallel_adj-tuned.json
```

## Citation

When citing this work please use the following citation:

```
@InProceedings{Nolle_2025_CRL,
  author       = {Nolle, Kim N. and Dusparic, Ivana and Cusack, Rhodri and Cahill, Vinny},
  title        = {Continual Reinforcement Learning for Cyber-Physical Systems: Lessons Learned and Open Challenges},
  booktitle    = {The 6th Multidisciplinary Conference on Reinforcement Learning and Decision Making},
  year         = {2025},
  pages        = {883--887},
  address      = {Dublin, Ireland},
  url = {https://drive.google.com/uc?export=download&id=1VBBaTHNfWV4aRYQXc6iJ43pGHRhOBydR},
  urldate = {2025-11-17},
}
```