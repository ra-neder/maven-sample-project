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
        archiveArtifacts: "target/*.jar"
        stash(name: "stash test", includes: "target/**")
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
