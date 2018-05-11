pipeline {
    agent none 
    stages {
        stage('Information') { 
            agent any
            steps {
                sh 'groups' 
            }
        }
        stage('Py Compile') { 
            agent {
                docker {
                    image 'python:2-alpine' 
                }
            }
            steps {
                sh 'python -m py_compile main.py' 
            }
        }
        stage('SonarQube Scanner') { 
            agent {
                docker {
                    image 'newtmitch/sonar-scanner:3.0.3-alpine' 
                }
            }
            steps {
                sh 'sonnar-scanner'
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}