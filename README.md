# Flight Booking Data Engineering Pipeline with Airflow and CICD



## Project Description



This project implements a data engineering pipeline to process flight booking data. It utilizes Apache Airflow for orchestration, Apache Spark for data transformation, and includes a Continuous Integration/Continuous Deployment (CI/CD) pipeline using GitHub Actions.









## Features



* Automated data ingestion/processing using Airflow.

* Scalable data transformation with Apache Spark.

* Environment-specific configurations (`dev` and `prod`).

* Automated testing and deployment via GitHub Actions (CI/CD).

* Includes sample `flight_booking.csv` data.



## Tech Stack







<img src="https://upload.wikimedia.org/wikipedia/commons/d/de/AirflowLogo.png" alt="Apache Airflow" width="150"/> <img src="https://spark.apache.org/images/spark-logo-trademark.png" alt="Apache Spark" width="150"/> <img src="https://github.githubassets.com/images/modules/logos_page/GitHub-Actions.png" alt="GitHub Actions" width="150"/> <img src="https://www.python.org/static/community_logos/python-logo-master-v3-TM.png" alt="Python" width="150"/> 




graph TB
    subgraph "Data Sources"
        A[Flight Booking CSV] -->|Upload| B[Cloud Storage]
    end
    
    subgraph "Orchestration"
        C[Cloud Composer/Airflow] -->|Orchestrates Pipeline| D[DAG Execution]
        D -->|Detects File| E[GCS File Sensor]
        E -->|Triggers| F[Dataproc Job]
    end
    
    subgraph "Processing"
        F -->|Executes| G[Spark Transformation Job]
        G -->|Transforms Data| H[Data Processing]
    end
    
    subgraph "Storage & Analytics"
        H -->|Writes to| I[BigQuery Tables]
        I -->|Stores| J[Transformed Data]
        I -->|Stores| K[Route Insights]
        I -->|Stores| L[Origin Insights]
    end
    
    subgraph "CI/CD Pipeline"
        M[GitHub Repository] -->|Push to Branch| N[GitHub Actions]
        N -->|Dev Branch| O[Deploy to DEV]
        N -->|Main Branch| P[Deploy to PROD]
    end
    
    B -->|Input Data| E
    P -->|Updates| C
    O -->|Updates| C



## Setup and Prerequisites

Before you begin, ensure you have the following installed and configured:

1.  **Git:** For cloning the repository.
2.  **Python 3.7+:** Ensure Python is installed.
3.  **Apache Airflow:** A running Airflow environment (local, Docker, or managed service). You'll need to place or configure Airflow to recognize the DAG file (`airflow_job/airflow_job.py`).
4.  **Apache Spark:** A Spark environment (local, cluster, or cloud-based) to execute the Spark job.
5.  **Java:** Spark requires Java to be installed.
6.  **GitHub Account:** To host the repository and use GitHub Actions.
7.  **GitHub Personal Access Token (PAT):** Configured for pushing code and potentially for CI/CD if needed for deployment steps (already addressed during pushing).

## Local Setup

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/jenvithmanduvaa/Flight-Booking-Airflow-CICD.git](https://github.com/jenvithmanduvaa/Flight-Booking-Airflow-CICD.git)
    cd Flight-Booking-Airflow-CICD
    ```

2.  **Switch to the `dev` branch:**
    ```bash
    git checkout dev
    ```

3.  **Place project files:** Ensure all necessary project files (like the ones you copied previously) are in this directory. If you followed the previous steps, they should already be here.

4.  **Install Python Dependencies:**
    Navigate to the directory containing your `requirements.txt` (if you have one; if not, you'll need to create one listing dependencies like `apache-airflow`, `pyspark`, etc.).
    ```bash
    # Example: If you have a requirements.txt in the root
    pip install -r requirements.txt
    # Or install individually
    # pip install apache-airflow pyspark ...
    ```

5.  **Configure Airflow:**
    Copy the `airflow_job.py` file into your Airflow DAGs folder so Airflow can discover it.
    ```bash
    # Example: Assuming your DAGs folder is ~/airflow/dags
    cp airflow_job/airflow_job.py ~/airflow/dags/
    ```
    Configure any necessary Airflow Connections or Variables as required by `airflow_job.py`.

6.  **Configure Environment Variables/Variables Files:**
    Review the `variables/dev/variables.json` and `variables/prod/variables.json` files. Ensure your Airflow/Spark setup can access the correct environment variables or load configurations from these files as intended by your code.

## Running the Pipeline

1.  **Start Airflow:** Ensure your Airflow scheduler and webserver are running.
2.  **Unpause the DAG:** In the Airflow UI, find the `airflow_job` DAG (or whatever name is defined in the Python file) and unpause it.
3.  **Trigger the DAG:** You can manually trigger the DAG from the Airflow UI or wait for its scheduled run.
4.  **Monitor:** Monitor the DAG run in the Airflow UI to check its progress and view logs if steps fail.

## CI/CD with GitHub Actions

The `.github/workflows/ci-cd.yaml` file defines the automated workflow that runs on GitHub Actions. Typically, this workflow will:

* Checkout the code.
* Set up Python.
* Install dependencies.
* Perform code quality checks (linting, formatting).
* Run tests (if you have them).
* (Potentially) Check DAG syntax.
* (Potentially) Build and push Docker images.
* (Potentially) Deploy to your target environment.

Check the `ci-cd.yaml` file for the specific steps implemented in your CI/CD pipeline. Monitor the "Actions" tab on your GitHub repository for the status of workflow runs triggered by your commits.

## Configuration

Configuration settings are managed in the `variables/` directory, separated by environment (`dev`, `prod`). Your Airflow and Spark jobs should be written to load configurations from the appropriate `variables.json` file based on the execution environment.

## Contributing

(Standard section - describe how others can contribute, e.g., fork the repo, create a branch, make changes, submit a pull request)

## License

(Standard section - specify the license under which your project is released, e.g., MIT, Apache 2.0, etc.)

---

This README provides a comprehensive overview. Remember to fill in any specifics required by your `airflow_job.py` or `spark_transformation_job.py` files, such as required environment variables, Airflow Connections/Variables, or specific Spark submission commands if applicable.
