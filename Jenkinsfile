pipeline {
agent any

options {
  buildDiscarder(logRotator(numToKeepStr: '10'))
  timestamps()
disableConcurrentBuilds()
}

environment {
  APP_NAME = 'hello-app'
  RUN_BY = 'webhook'
}

stages {
  stage('Hello') {
    steps {
      echo "Starting ${env.APP_NAME} by ${env.RUN_BY}"
}
}
}

post {
  success { echo ' pipeline succeeded' }
  failure { echo ' pipeline failed' }
  always { echo ' Build URL: ${env.BUILD_URL' }
}
}
