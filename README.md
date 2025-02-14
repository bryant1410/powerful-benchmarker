<h1>
<a href="https://github.com/KevinMusgrave/powerful-benchmarker">
<img alt="Powerful Benchmarker" src="https://github.com/KevinMusgrave/powerful-benchmarker/blob/domain-adaptation/imgs/Logo.png">
</a>
</h1>

## Which git branch should you checkout?

- The [domain-adaptation](https://github.com/KevinMusgrave/powerful-benchmarker/tree/domain-adaptation) branch contains code for:
  - [Three New Validators and a Large-Scale Benchmark Ranking for Unsupervised Domain Adaptation](https://arxiv.org/pdf/2208.07360.pdf)
- The [metric-learning](https://github.com/KevinMusgrave/powerful-benchmarker/tree/metric-learning) branch contains code for:
  - [A Metric Learning Reality Check](https://arxiv.org/pdf/2003.08505.pdf)
  
Currently I can provide technical support (help with code, bug fixes etc.) for the `domain-adaptation` branch only.

## Installation

Clone this repo:
```
git clone https://github.com/KevinMusgrave/powerful-benchmarker.git
```

Then go into the folder and install the required packages:
```
cd powerful-benchmarker
pip install -r requirements.txt
```

## Set paths in `constants.yaml`

- `exp_folder`: experiments will be saved as sub-folders inside of `exp_folder`
- `dataset_folder`: datasets will be downloaded here. For example, `<dataset_folder>/mnistm`
- `conda_env`: (optional) the conda environment that will be activated for slurm jobs
- `slurm_folder`: slurm logs will be saved to `<exp_folder>/.../<slurm_folder>`
- `gdrive_folder`: (optional) the google drive folder to which logs can be uploaded


## Folder organization

Visit each folder to view its readme file.

| Folder | Description |
| - | - |
| [`latex`](https://github.com/KevinMusgrave/powerful-benchmarker/tree/domain-adaptation/latex) | Code for creating latex tables from experiment data.
| [`notebooks`](https://github.com/KevinMusgrave/powerful-benchmarker/tree/domain-adaptation/notebooks) | Jupyter notebooks
| [`powerful_benchmarker`](https://github.com/KevinMusgrave/powerful-benchmarker/tree/domain-adaptation/powerful_benchmarker) | Code for hyperparameter searches for training models.
| [`scripts`](https://github.com/KevinMusgrave/powerful-benchmarker/tree/domain-adaptation/scripts) | Various bash scripts, including scripts for uploading logs to google drive.
| [`unit_tests`](https://github.com/KevinMusgrave/powerful-benchmarker/tree/domain-adaptation/unit_tests) | Tests to check if there are bugs.
| [`validator_tests`](https://github.com/KevinMusgrave/powerful-benchmarker/tree/domain-adaptation/validator_tests) | Code for evaluating validation methods (validators).


## Useful top-level scripts

### delete_slurm_logs.py
Delete all slurm logs:
```
python delete_slurm_logs.py --delete
```

Or delete slurm logs for specific experiments groups. For example, delete slurm logs for all experiment groups starting with "officehome":
```
python delete_slurm_logs.py --delete --exp_group_prefix officehome
```
---
### kill_all.py
Kill all model training jobs:
```
python kill_all.py
```
Or kill all validator test jobs:
```
python kill_all.py --validator_tests
```
---
### print_progress.py
Print how many hyperparameter trials are done:
```
python print_progress.py
```

Include a detailed summary of validator test jobs:
```
python print_progress.py --with_validator_progress
```

Save to `progress.txt` instead of printing to screen:
```
python print_progress.py --save_to_file progress.txt
```
---
### simple_slurm.py
A simple way to run a program via slurm. 

For example, run `collect_dfs.py` for all experiment groups starting with "office31", using a separate slurm job for each experiment group:
```
python simple_slurm.py --command "python validator_tests/collect_dfs.py" --slurm_config_folder validator_tests \
--slurm_config a100 --job_name=collect_dfs --cpus-per-task=16 --exp_group_prefix office31
```

Or run a program without considering experiment groups at all:
```
python simple_slurm.py --command "python validator_tests/zip_dfs.py" --slurm_config_folder validator_tests \
--slurm_config a100 --job_name=zip_dfs --cpus-per-task=16
```
---
### upload_logs.py
Upload slurm logs and experiment progress to a google drive folder at regular intervals (the default is every 2 hours):
```
python upload_logs.py
```
Set the google drive folder in `constants.yaml`.


## Logo
Thanks to [Jeff Musgrave](https://www.designgenius.ca/) for designing the logo.


## Citing the paper

```
@article{Musgrave2022ThreeNew,
  title={Three New Validators and a Large-Scale Benchmark Ranking for Unsupervised Domain Adaptation},
  author={Kevin Musgrave and Serge J. Belongie and Ser Nam Lim},
  journal={ArXiv},
  year={2022},
  volume={abs/2208.07360}
}
```
