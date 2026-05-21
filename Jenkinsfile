pipeline {
  agent any
  tools {
    maven "maven-3.9"
  }
  stages {
    stage("build jar") {
      steps {
        echo "building the application..."
        sh 'mvn package'
      }
    }
    stage("build image") {
      steps {
        echo "building the docker image..."
        withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'PASS', usernameVariable: 'USER')]){
          sh 'docker build -t shivangjnv/java-maven-app:2.0 .'
          sh 'echo $PASS | docker login -u $USER --password-stdin'
          sh 'docker push shivang/java-maven-app:2.0'
        }
      }
    }
    stage("deploy") {
      steps {
        echo "deploying the application..."
      }
    }
  }
}