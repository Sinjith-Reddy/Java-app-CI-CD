pipeline {
  agent {node: 'java'}
  environment {
    tool maven 'MAVEN_HOME'
  }
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: https://github.com/Sinjith-Reddy/Java-app-CI-CD.git
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
      post {
        success {
          archiveArtifacts artifacts: '**/target/*.jar'
        }
      }
    }
    stage('Maven test') {
      steps{
        sh 'mvn test'
      }
    }
  }
}
