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
                helm upgrade evergreen-helm && 
                helm upgrade helm-grafana --values ./helm-values-grafana.yaml &&
                helm upgrade helm-prometheus --values ./helm-values-prometheus.yaml
                """
            }
        }
    }
}