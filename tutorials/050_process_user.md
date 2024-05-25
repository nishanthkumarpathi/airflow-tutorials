# Process User

## Learning Objectives

After completing this coding exercise, you will able to:

* Fetch data from previous tasks - Process data using pandas
* Run a Python function with the PythonOperator

## Instructions

Within your DAG `user_processing`, add the task that processes data fetched by extract_user using the [PythonOperator](https://airflow.apache.org/docs/apache-airflow/stable/howto/operator/python.html).

This task must:

- Have the name "process_user"
    
- Call the pre-defined function _process_user
    
    - The function _process_user fetches data from the task extract_user using XCOMs. You will learn more about XCOMs later in the course, for now, think of XCOMs as a way to share data between tasks.
        
        The the function uses json_normalize to extract and format the data to store it into a CSV file.
        
- Add the following dependencies **after** the task: `extract_user >> process_user`

## Steps

Step 1: Import the PythonOperator and json_normalize

```python
from pandas import json_normalize # used in _process_user
```

Step 2: Define the function _process_user

```python
# The python function to call
def _process_user(ti):
    user = ti.xcom_pull(task_ids="extract_user") # fetch data pushed by the previous task extract_user
    user = user['results'][0]
    processed_user = json_normalize({
        'firstname': user['name']['first'],
        'lastname': user['name']['last'],
        'country': user['location']['country'],
        'username': user['login']['username'],
        'password': user['login']['password'],
        'email': user['email'] })
    processed_user.to_csv('/tmp/processed_user.csv', index=None, header=False)

```

Step 3: Add the PythonOperator task to the DAG

```python
    process_user = PythonOperator(
        task_id='process_user',
        python_callable=_process_user
    )
    
    extract_user >> process_user
```

Step 4: Run the DAG and verify the CSV file
