pipeline {
    agent any

    environment {
        TEST="test-variable"
    }

    stages {
        stage('Build') {
            steps {
                sh 'echo $TEST'
            }
        }
        stage('Deploy') {
            steps {
                sh """
                aws eks --region us-east-1 update-kubeconfig --name tinker-cluster
                kubectl config get-contexts
                helm repo add grafana https://grafana.github.io/helm-charts
                helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
                helm repo update
                helm upgrade evergreen-helm ./evergreen-chart  && 
                helm upgrade helm-grafana grafana/grafana --values ./helm-values-grafana.yaml &&
                helm upgrade helm-prometheus prometheus-community/prometheus --values ./helm-values-prometheus.yaml
                """
            }
        }
    }
}