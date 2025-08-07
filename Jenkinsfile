pipeline {
    agent any

    environment {
        IMAGE_NAME = "java-login-app"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/NotHarshhaa/DevOps-Projects.git'
            }
        }

        stage('Build Maven Project') {
            steps {
                dir('DevOps-Project-01/Java-Login-App') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                dir('DevOps-Project-01/Java-Login-App') {
                    script {
                        dockerImage = docker.build("${IMAGE_NAME}")
                    }
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker rm -f java-login-container || true'
                    dockerImage.run("-d -p 8080:8080 --name java-login-container")
                }
            }
        }
    }
}
