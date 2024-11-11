pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "dakui/dockerized-cicd-pipeline:latest"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Dakuii/dockerized-cicd-pipeline.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the application...'
                // Add any test commands here
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    script {
                        docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-creds') {
                            docker.image(DOCKER_IMAGE).push()
                        }
                    }
                }
            }
        }
    }
}

