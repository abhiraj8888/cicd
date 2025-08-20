pipeline {
  agent any    // Run this pipeline on any available Jenkins agent (node)

  stages {
    stage('stage1') {   // Define a stage named "stage1"
      steps {
        sh 'systemctl status jenkins'   // Run a shell command on the agent
        echo "hello"                    // Print "hello" to Jenkins console log
      }
    }
  }
}
