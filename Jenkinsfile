pipeline {
  agent any
  
  stages {
    stage('build') {
      steps {
        sh 'mvn clean install'
      }
      post {
        success {
          
          stash includes: "target/*.jar", name: "target"
        }
      }
    }
    stage('publish') {
      steps {
        unstash "target"
        archiveArtifacts 'target/*.jar'
        sshPublisher(publishers: [sshPublisherDesc(configName: 'myserver', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: 'target', sourceFiles: 'target/*.jar')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
      }
    }
    stage('integration test') {
      steps {
        sh 'curl -i -H "Accept: application/json" -H "Content-Type: application/json" -X GET http://localhost:8081/employees'
      }
    }
  }
}
