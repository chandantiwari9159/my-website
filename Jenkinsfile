pipeline {
    agent any

    environment {
        IMAGE_NAME = 'chandantiwari9159/my-web-app'
        TAG = 'latest'
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/chandantiwari9159/my-website'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:${TAG}")
                }
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'SharadShandilya') {
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
