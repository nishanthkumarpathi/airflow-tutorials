# Basic Dag

### Learning Objective:

- Create a DAG object following best practices
- Define when to trigger your DAG
- Give a unique name to your DAG to identify it on the UI

### Simple Airflow DAG

Write a simple Airflow DAG with no tasks and dependencies that must:

- Use the context manager "with" to instantiate the DAG class
- Have a unique identifier "user_processing"
- Start the on January 1st, 2023
- Run every day at midnight using a cron preset
- Have catchup=False as we don't want to backfill missed runs (yet). You will see that later in the course.

### Steps

Step 1: Create a new Python file in the dags folder named user_processing.py

Step 2: Copy and paste the following code into the user_processing.py file

```python
from airflow import DAG
from datetime import datetime
 
with DAG(
    dag_id="user_processing",
    start_date=datetime(2023, 1, 1),
    schedule_interval="@daily",
    catchup=False
) as dag:
    pass
```
Wait for couple of Minutes and refresh the UI to see the DAG user_processing.

When you run the DAG, you will see that it will not have any tasks to run.




