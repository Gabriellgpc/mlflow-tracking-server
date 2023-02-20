# mlflow-tracking-server

MLflow is an open source platform for managing the end-to-end machine learning lifecycle. It tackles four primary functions:
- Tracking experiments to record and compare parameters and results (MLflow Tracking).
- Packaging ML code in a reusable, reproducible form in order to share with other data scientists or transfer to production (MLflow Projects).
- Managing and deploying models from a variety of ML libraries to a variety of model serving and inference platforms (MLflow Models).
- Providing a central model store to collaboratively manage the full lifecycle of an MLflow Model, including model versioning, stage transitions, and annotations (MLflow Model Registry).

For more information refer to
- [MLFlow Quickstart](https://www.mlflow.org/docs/latest/quickstart.html)
- [Tutorials and Examples](https://www.mlflow.org/docs/latest/tutorials-and-examples/index.html)

# MLflow Tracking
*MLflow Tracking* is an API and UI for logging parameters, code versions, metrics, and artifacts when running your machine learning code and for later visualizing the results. You can use MLflow Tracking in any environment (for example, a standalone script or a notebook) to log results to local files or to a server, then compare multiple runs. Teams can also use it to compare results from different users.

# Setup
This setup is heavly based on [Toumash's work](https://github.com/Toumash/mlflow-docker) where a `docker-compose` [project](docker-compose.yml) is proposed to orchestrate `database`, `FTP server`, `mlflow server` and `reverse-proxy` images.

In order to configure `mlflow server instance`, follow these steps:

1. Create the file `.env` and set the following variables (please refer to [Server configuration](https://docs.google.com/document/d/1yQPpjrVhb7_2PgzMvjHISPA8rnItH-gCmlL_IJcqJGE/edit?usp=sharing)):
 - `DB_USER` - username for internal MLflow tracking database (arbitrary)
 - `DB_PW` - password for internal MLflow tracking database (arbitrary)
 - `DB_ROOTPW` - root password for internal ML Flow tracking database (arbitrary)
 - `MLFLOW_SERVER_IP` - remote MLflow tracking instance
 - `MLFLOW_TRACKING_USERNAME`- MLflow proxy authentication username
 - `MLFLOW_TRACKING_PASSWORD` - MLflow proxy authentication password
 - `ARTIFACT_PATH` - File Storage where artifacts will be stored
 - `FTP_USER` - username for internal FTP server
 - `FTP_PASS` - password for internal FTP server


2. Export `MLFLOW_TRACKING_USERNAME` and `MLFLOW_TRACKING_PASSWORD` variables

3. Run `setup.sh` to install dependencies and create `reverse-proxy` authentication file

# Start MLFlow Tracking server (daemon mode)
Build docker images and start containers using `docker-compose`:
```
$ docker-compose up -d --build
```

# Check start up logs for errors
```
$ docker-compose logs -f
```

# Verify tracking server ui
Open a web browser at http://<MLFLOW_SERVER_IP> and authenticate with <MLFLOW_TRACKING_USERNAME> and <MLFLOW_TRACKING_PASSWORD>


# Stop and remove containers
```
$ docker-compose rm --stop --force
```


# References
- https://www.mlflow.org/docs/latest/index.html
- https://www.mlflow.org/docs/latest/concepts.html
- https://www.mlflow.org/docs/latest/tracking.html
- https://github.com/Toumash/mlflow-docker
- https://towardsdatascience.com/deploy-mlflow-with-docker-compose-8059f16b6039