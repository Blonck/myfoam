# Idea

This should contain every step to bring a machine-learning model to life.
This contains:
1. Exploring the data (TODO)
2. Building preliminary first model (TODO)
3. Setting up data pipelines (TODO)
4. Developing an API for the model (TODO)
5. Creating a docker image for the API (TODO)
6. Trying different models and tune hyperparameters (TODO)
7. Deploying the model to (TODO)
    * AWS
    * Google cloud
    * Microsoft Azure

# Dataset

Bank marketing campaign data from [https://archive.ics.uci.edu/ml/datasets/Bank+Marketing#]
* freely available
* maybe a bit boring matketing data, but this is not about the data
* not too easy classification problem as it is a imbalanced dataset, missing values, etc


# Setup the working environment

## install miniconda
- see [https://conda.io/projects/conda/en/latest/user-guide/install/index.html]
- download python3 installer from [https://docs.conda.io/en/latest/miniconda.html#linux-installers]
- install it via `bash Miniconda3-latest-Linux-x86_64.sh`

## create new conda environment

- use model2cloud.yml to create new environment
`conda env create --file model2cloud.yml`
or even faster use mamba
```
conda install mamba -n base -c conda-forge
mamba env create --file model2cloud.yml
```

- activate environment
`conda activate model2cloud`

- start jupyter 
`jupyter notebook`

# EDA

- 01_EDA.ipynb
* no NAs
* no special treatment necessary

# Model Building

- 02_FirstModel.ipynb
* simple RF
* metric: balanced accuracy

# Pipelining

# Into the cloud

## AWS

## Azure

## Google

##
