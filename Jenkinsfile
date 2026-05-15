pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "pierredja/pierre-python-app"
    }

    stages {
        stage('Pierre - Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }

        stage('Pierre - Login to Dockerhub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Pierre - Push image to Dockerhub') {
            steps {
                sh 'docker push $DOCKER_IMAGE:latest'
            }
        }
    }
}
