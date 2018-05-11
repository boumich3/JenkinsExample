pipeline {
    agent none 
    stages {
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