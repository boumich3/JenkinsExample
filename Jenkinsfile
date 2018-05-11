pipeline {
    agent none 
    stages {
        stage('Build') { 
            agent {
                docker {
                    image 'newtmitch/sonar-scanner:3.0.3-alpine' 
                }
            }
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