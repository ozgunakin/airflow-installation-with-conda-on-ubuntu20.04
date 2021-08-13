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

## Step 4 - Install Necessary Packages

```text
sudo apt-get install libmysqlclient-dev
pip install mysqlclient
```

## Step 5 - Install Airflow

We will install airflow 2.1.0 using conda-forge to our airflowenv.

```text
conda install -c conda-forge airflow=2.1.0
```

## Step 6 - Configure Environment Variables

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

## Step  7 - Install MySQL \(If you don't already have it\)

You can find a step by step guide on how to install MySQL here [https://github.com/ozgunakin/mysql-installation-on-ubuntu20.04](https://github.com/ozgunakin/mysql-installation-on-ubuntu20.04)

## Step 8 - Create an Airflow User in MySQL

You need to create an airflow database and a user who is permitted to write on this table.

* [x] Create an airflow database

```text
sudo mysql

CREATE DATABASE airflow;
```

* [x] Create and authorize an airflow user.

```text
CREATE USER 'airflow'@'%' IDENTIFIED BY 'sczq6vP!';
GRANT ALL PRIVILEGES ON airflow.* TO 'airflow'@'%' WITH GRANT OPTION;
```

## Step 9 - Install RabbitMQ \(If you want to create an Airflow Cluster, otherwise you don't need it\)

You can find a step by step guide on how to install RabbitMQ here [https://github.com/ozgunakin/rabbitmq-installation-on-ubuntu20.04](https://github.com/ozgunakin/rabbitmq-installation-on-ubuntu20.04)

## Step 10 - Create an Airflow User in RabbitMQ  \(If you want to create an Airflow Cluster, otherwise you don't need it\)

You need to create and authorize an airflow user in RabbitMQ.

```text
sudo rabbitmqctl add_user airflow 5Cmj5bw8
sudo rabbitmqctl set_user_tags airflow administrator
```

## Step 11 - Create a Virtual Host in RabbitMQ  \(If you want to create an Airflow Cluster, otherwise you don't need it\)

* [x] Go to RabbitMQ URL on your browser. [http://YOUR\_IP:15672](http://10.115.209.137:15672/#/users)
* [x] Click the Admin button. Then click the virtual hosts button which is placed right on the page.

![](.gitbook/assets/image.png)

* [x] Click "Add a new virtual host" and enter your hostname as airflow. Then click "Add a virtual host".

![](.gitbook/assets/image%20%281%29.png)

## Step 12 - Configure Airflow

* [x] Open the airflow configuration file.

```text
sudo nano /data/airflow/airflow.cfg
```

* [x] Change the following lines on the configuration file.
* executor = LocalExecutor
* sql\_alchemy\_conn = mysql://airflow:sczq6vP!@localhost:3306/airflow
* broker\_url = amqp://airflow:5Cmj5bw8@10.115.209.137:5672/airflow \#This is needed if you are creating airflow cluster
* result\_backend = db+mysql://airflow:sczq6vP!@10.115.209.137:3306/airflow

## Step 13 - Inıtilaze Airflow db

```text
airflow db init
```

## Step 14 - Run Airflow

* [x] Run webserver. 

```text
airflow webserver
```

* [x] Run scheduler asa daemon.

```text
airflow scheduler -D
```

