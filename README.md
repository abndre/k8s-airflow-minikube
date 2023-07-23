minikube kubectl -- apply -f airflow-config.yml

minikube dashboard

mkdir dags
mkdir logs
mkdir data

minikube mount ./dags/:/data/dags
minikube mount ./data/:/data/data
minikube mount ./logs/:/data/logs


minikube ssh

ls /data/dags

# docker etapa

eval $(minikube -p minikube docker-env)
docker build -t airflow-alura .


# AIRFLOW INSTALL

helm upgrade --install airflow apache-airflow/airflow --namespace airflow -f override-values.yml

minikube kubectl -- port-forward svc/airflow-webserver 8080:8080 --namespace airflow