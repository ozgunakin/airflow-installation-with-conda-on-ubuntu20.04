# Apache Airflow Installation with Conda

This repository is a guide for Apache Airflow installation on Ubuntu 20.04 using Anaconda.

## Step 1 - Install Anaconda

You can find a step by step guide on how to install anaconda here [https://github.com/ozgunakin/anaconda-installation-on-ubuntu20.04](https://github.com/ozgunakin/anaconda-installation-on-ubuntu20.04)

## Step 2 - Create a Conda Environment

Creating an environment is important to easily manage pip packages.

```text
conda create --name airflowenv

conda activate airflowenv
```

## Step 3 - Create an Airflow Directory \(Optional\)

Actually, you don't need to create a directory for airflow, because airflow automatically creates it under your home directory. In our case, we want to store airflow files line dags, configs, and PID's in another location\(/data/airflow\). That is why we are creating a directory for it.

```text
mkdir /data/airflow
```

## Step 4 - Install Airflow

We will install airflow 2.1.0 using conda-forge to our airflowenv.

```text
conda install -c conda-forge airflow=2.1.0
```

## Step 5 - Configure Environment Variables

We need to set AIRFLOW\_HOME and AIRFLOW\_CONFIG paths in .bashrc file of our user because we don't want to use the default home directory.

```text
nano ~/.bashrc
```

* [x] Enter following lines into .bashrc file and save the file
* export AIRFLOW\_HOME=/data/airflow
* export AIRFLOW\_CONFIG=/data/airflow/airflow.cfg

```text
source ~/.bashrc
```

## Step 6 - Install MySQL \(If you don't already have\)

You can find a step by step guide on how to install anaconda here [https://github.com/ozgunakin/mysql-installation-on-ubuntu20.04](https://github.com/ozgunakin/mysql-installation-on-ubuntu20.04)

## Step 7 - Create Airflow User in MySQL



