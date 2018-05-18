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
            agent any
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    script {
                        def sonarqubeScannerHome = tool name: 'SonarQube Scanner', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
                        sh "${sonarqubeScannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
        stage("Quality Gate"){
            steps {
                timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
                    script {
                        def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
                        if (qg.status != 'OK') {
                            error "Pipeline aborted due to quality gate failure: ${qg.status}"
                        }
                    }
                }
            }
        }
    }
}