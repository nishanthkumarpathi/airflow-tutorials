# Extract Users

## Learning Objectives
After completing this coding exercise, you will able to:

- Fetch data from an API in your DAG
- Use the SimpleHttpOperator to interact with web pages

## Instructions
Within your DAG user_processing, add a third task that fetches data from an the API using the SimpleHttpOperator.

This task must:
    - Have the name "extract_user"
    - Use the connection "user_api" that you've created previously
    - Reach the endpoint api/ with the method GET
    - Filter the response by loading it with json.loads
    - Log the response in the Airflow UI

Learn more about the SimpleHttpOperator ![here](https://airflow.apache.org/docs/apache-airflow-providers-http/stable/_api/airflow/providers/http/operators/http/index.html)

## Steps

Step 1: Import the SimpleHttpOperator and json

```python
from airflow.providers.http.operators.http import SimpleHttpOperator
 
import json
```

Step 2: Add the SimpleHttpOperator task to the DAG

```python
    extract_user = SimpleHttpOperator(
        task_id='extract_user',
        http_conn_id='user_api',
        endpoint='api/',
        method='GET',
        response_filter=lambda response: json.loads(response.text),
        log_response=True
    )
```