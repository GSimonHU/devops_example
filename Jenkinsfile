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
                sh 'echo Deploy'
            }
        }
    }
}