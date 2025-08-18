pipeline {
    agent any

    environment {
        DOCKER_HUB = "abhidocker06/jenkinsrepo"   // Change to your repo
        DOCKER_CREDENTIALS = credentials('docker-hub-cred')  // Jenkins credential ID
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/abhiraj8888/cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_HUB:$BUILD_NUMBER .'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    sh 'echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKER_CREDENTIALS_USR --password-stdin'
                    sh 'docker push $DOCKER_HUB:$BUILD_NUMBER'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Simple deployment: run container locally (you can expand to Kubernetes later)
                    sh 'docker run -d -p 5000:5000 $DOCKER_HUB:$BUILD_NUMBER'
                }
            }
        }
    }
}
