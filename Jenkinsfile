pipeline {
  agent {
    node {
      label 'nuc'
    }
  }
  tools {
    maven 'm3'
  }
  stages {
    stage ('Build') {
      steps {
        sh "mvn clean install"
        archiveArtifacts "target/*.jar"
        stash(name: "stash test", includes: "target/**")
      }
    }
    stage ('Approval') {
      agent none
      steps {
        input(message: "Ok to continue?", ok: "Yes") 
      }
    }
    stage ('Test') {
      steps {
        unstash "stash test"
        sh '''
        ls . && ls target/**
        '''
      }
    }
  }
}
