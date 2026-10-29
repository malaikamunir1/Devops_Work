pipeline {
    agent any
    
    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials'
        IMAGE_NAME = 'areebakhan49' // Agar aapka Docker Hub username different hai toh 'malaikamunir1' ki jagah wo likhein
    }
    
    stages {
        stage('Stage 1: Pull code from GitHub') {
            steps {
                checkout scm
            }
        }
        
        stage('Stage 2: Build Docker image') {
            steps {
                script {
                    app = docker.build("${IMAGE_NAME}:${env.BUILD_NUMBER}")
                }
            }
        }
        
        stage('Stage 3: Push image to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        app.push("latest")
                        app.push("${env.BUILD_NUMBER}")
                    }
                }
            }
        }
    }
    
    post {
        always {
            echo "Pipeline execution finished!"
        }
    }
}
