#!/user/bin/env groovy

library identifier: 'jenkins-shared-library@main', retriever: modernSCM([
  $class: 'GitSCMSource',
  remote: 'https://github.com/shivang-jnv/jenkins-shared-library.git',
  credentialsId: 'github-credentials'
])

def gv

pipeline {
  agent any
  tools {
    maven "maven-3.9"
  }
  stages {
    stage("init"){
      steps {
        script {
          gv = load "script.groovy"
        }
      }
    }
    stage("build jar") {
      steps {
        script{
          buildJar()
        }
      }
    }
    stage("build and push image") {
      steps {
        script {
          buildImage 'shivangjnv/java-maven-app:3.0'
          dockerLogin()
          dockerPush 'shivangjnv/java-maven-app:3.0'
        }
      }
    }
    stage("deploy") {
      steps {
        script {
          gv.deployApp()
        }
      }
    }
  }
}