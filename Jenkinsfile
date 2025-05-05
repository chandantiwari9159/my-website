pipeline {
    agent any

    environment {
        IMAGE_NAME = 'chandantiwari9159/my-web-app'
        TAG = 'latest'
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/chandantiwari9159/my-website.git' 
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${my-web-app:latest}:${TAG}")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials-id') {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    sh "docker stop myweb || true"
                    sh "docker rm myweb || true"
                    sh "docker run -d -p 8080:80 --name myweb ${IMAGE_NAME}:${TAG}"
                }
            }
        }
    }
}
