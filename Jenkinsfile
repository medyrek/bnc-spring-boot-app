pipeline {
  agent any
  
  stages {
    stage('build') {
      steps {
        sh 'mvn clean install'
      }
    }
    stage('integration test') {
      steps {
        sh 'curl localhost:8081'
      }
    }
  }
}
