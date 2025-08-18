pipeline {
    agent any

    environment {
        DOCKER_HUB = "abhidocker06/cicd" // Your Docker Hub repo
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
                    // Build image with Jenkins build number
                    sh 'docker build -t $DOCKER_HUB:$BUILD_NUMBER .'
                    // Also tag latest
                    sh 'docker tag $DOCKER_HUB:$BUILD_NUMBER $DOCKER_HUB:latest'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Safer way to use credentials
                    withCredentials([usernamePassword(credentialsId: 'da188a66-95bf-451d-8f35-e2541db67ab4', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh 'docker push $DOCKER_HUB:$BUILD_NUMBER'
                        sh 'docker push $DOCKER_HUB:latest'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Stop/remove old container if running
                    sh 'docker rm -f myapp || true'
                    // Run new container
                    sh 'docker run -d --name myapp -p 5000:5000 $DOCKER_HUB:$BUILD_NUMBER'
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finished (success or failure)."
        }
        success {
            echo "Deployment successful ✅"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}
