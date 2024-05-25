# Store the User

## Learning Objectives


After completing this coding exercise, you will able to: 

* Interact with third-party services using Hooks 
* Run Python functions

## Instructions

Within your DAG `user_processing`, add the last task to store the processed data in the CSV file in your Postgres database. For that, the task needs to run the Python function _store_user.

This task must:

- Have the name "store_user"
    
- Call the pre-defined function _store_user
    
    - This function uses the PostgresHook to interact with Postgres. Hooks help abstract away the complexity of interacting with third-party tools and services. They usually give access to additional methods you might not have access to from the corresponding Operator. Here, we use copy_expert to export data from a CSV file into a Postgres table which isn't available with the PostgresOperator.


## Steps

### Step 1: Import the PostgresHook

```python
from airflow.providers.postgres.hooks.postgres import PostgresHook
```

### Step 2: Add the PythonOperator task to the DAG

```python
    store_user = PythonOperator(
        task_id='store_user',
        python_callable=_store_user
    )
```

### Step 3: Define the function _store_user

```python
def _store_user():
    hook = PostgresHook(postgres_conn_id='postgres')
    hook.copy_expert(
        sql="COPY users FROM stdin WITH DELIMITER as ','",
        filename='/tmp/processed_user.csv'
    )
```

### Step 4: Update the Sequence of Tasks

```python
    create_table >> is_api_available >> extract_user >> process_user >> store_user
```

### Step 5: Execute the DAG in the Airflow UI

- Trigger the DAG `user_processing` in the Airflow UI
- Verify the DAG runs successfully and the data is stored in the Postgres database

### Step 6: Verify CSV file in the Worker

```bash
docker exec -it airflow-tutorials-airflow-worker-1 /bin/bash
```

```bash
ls /tmp/
```

### Step 7: Verify the Postgres Database

```bash
docker exec -it airflow-tutorials-postgres-1 /bin/bash
```

```bash
psql -U airflow
```

```sql
SELECT * FROM users;
```

Now you have completed user_processing DAG