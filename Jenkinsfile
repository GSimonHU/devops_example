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
                kubectl config get-contexts
                helm upgrade evergreen-helm ./evergreen-chart  && 
                helm upgrade helm-grafana grafana/grafana --values ./helm-values-grafana.yaml &&
                helm upgrade helm-prometheus prometheus-community/prometheus --values ./helm-values-prometheus.yaml
                """
            }
        }
    }
}