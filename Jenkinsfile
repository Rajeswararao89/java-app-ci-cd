pipeline {
    agent any

    environment {
        IMAGE_NAME = 'java-login-app'
        CONTAINER_NAME = 'java-login-container'
        APP_PORT = '8080'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Rajeswararao89/java-app-ci-cd.git'
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
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    sh "docker run -d -p ${APP_PORT}:${APP_PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME}"
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Application built and deployed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check logs.'
        }
    }
}
