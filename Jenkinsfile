pipeline {
  agent any
  stages {
    stage('step1') {
      steps {
        echo "hello jenkinsfile"
        sh 'pwd'
        sh 'whoami'
      }
    }
    stage('step2') {
      steps {
        echo "hello again, jenkinsfile"
        sh 'who'
      }
    }
  }
}
