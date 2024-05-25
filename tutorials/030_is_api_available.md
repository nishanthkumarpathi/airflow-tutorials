# Implement the sensor is_api_available

## Learning Objectives

After completing this coding exercise, you will able to:
- Wait for a condition to be met before executing the next task
- Check if an API is available or not
- Configure Sensors in DAGs

## Instructions

Within your existing DAG user_processing, add your second task to check if the API is available or not:

- Go to the Airflow UI (on your machine localhost:80880) and create the following connection:
    - Name: user_api
    - Connection type: HTTP
    - Host: https://randomuser.me/

- After the task create_table, create a new task with:
    - The name is_api_available
    - That uses the connection you've created in the previous step
    - With the endpoint api/

## Steps

### Step 1: Add the API Connection

```python
from airflow.providers.http.sensors.http import HttpSensor
```

```python
    is_api_available = HttpSensor(
        task_id='is_api_available',
        http_conn_id='user_api',
        endpoint='api/'
    )
```





