pipeline {
    agent none 
    stages {
        stage('Build') { 
            agent any
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    sh 'sonnar-scanner'
                }
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