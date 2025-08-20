pipeline {
  agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '10')) // keep last 10 builds
    timestamps()                                   // show times in logs
    disableConcurrentBuilds()                      // avoid overlapping runs
  }

  environment {
    APP_NAME = 'hello-app'
    RUN_BY   = 'webhook'
  }

  stages {
    stage('Hello') {
      steps {
        echo "Starting ${env.APP_NAME} by ${env.RUN_BY}"
      }
    }
  }

  post {
    success { echo '✅ Pipeline Succeeded' }
    failure { echo '❌ Pipeline Failed' }
    always  { echo "Build URL: ${env.BUILD_URL}" }
  }
}
