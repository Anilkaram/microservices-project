pipeline {
    agent any

    stages {
        stage('Build & Tag Docker Image') {
            steps {
                sh "docker build -t anildoc143/adservice:latest ."
            }
        }

        stage('Scan Docker Image') {
            steps {
                sh 'trivy image --exit-code 1 --severity CRITICAL anildoc143/adservice:latest || exit 1'
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                        sh "docker push anildoc143/adservice:latest "
                    }
                }
            }
        }
    }
}
