pipeline {
    agent { docker { image 'python:3.5-alpine' } }
    stages {
        stage('build') {
            steps {
                bat 'python --version'
            }
        }
    }
}