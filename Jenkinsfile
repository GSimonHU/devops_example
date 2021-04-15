pipeline {
    agent any

    environment {
        GRAFANA_USERNAME="evergreen"
        GRAFANA_PASSOWRD="password"
    }

    stages {
        stage('Cluster Setup') {
            steps {
                sh """
                aws eks --region us-east-1 update-kubeconfig --name tinker-cluster
                kubectl config get-contexts
                """
            }
        }
        stage('Source') {
            steps {
                sh """
                helm repo add grafana https://grafana.github.io/helm-charts
                helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
                helm repo update
                """
            }
        }
        stage('Build') {
            steps {
                sh """
                kubectl delete secret grafana-secret
                kubectl create secret generic grafana-secret --from-literal=admin-user=$GRAFANA_USERNAME --from-literal=admin-password=$GRAFANA_PASSOWRD
                helm upgrade evergreen-helm ./evergreen-chart --install
                helm upgrade helm-grafana grafana/grafana --values ./helm-values-grafana.yaml --install
                helm upgrade helm-prometheus prometheus-community/prometheus --values ./helm-values-prometheus.yaml --install
                """
            }
        }
    }
}