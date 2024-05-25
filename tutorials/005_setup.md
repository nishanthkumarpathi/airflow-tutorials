# Setup Airflow Infrastrcture

## Prerequisites

* Docker Desktop installed on your machine. If you don't have it installed, you can download it from [here](https://www.docker.com/products/docker-desktop).


## Setup Guide

### Docker Compose File

Copy or Download the `docker-compose.yml` file from the airflow documenation.

### Create a `.env` file

Create a `.env` file in the same directory as the `docker-compose.yml` file. Add the following environment variables to the `.env` file.

```bash
AIRFLOW_IMAGE_NAME=apache/airflow:2.4.2
AIRFLOW_UID=50000
```

### Start the Airflow Services

Run the following command to start the Airflow services.

```bash
docker-compose up -d
```

### Added Airflow Pre-requisites Folders

Only do this step, if the airflow services are not running, due to the folders not being created.

- dags
- plugins
- logs

### .gitignore files

```yaml
# .gitignore
/logs
.env
.pyc
__pycache__/
```