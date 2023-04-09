pipeline {
  // to specify on which node you want to run this
  agent { label 'java'} 
  environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-cred-ID from Jenkins')
    REMOTE_SERVER = '52.73.28.146'
    REMOTE_USER =  credentials('user credentials-ID from Jenkins')
  }
  
  /* if multiple versions are installed and you want to use specific version then make use of tools attribute
  create a installation in 'Jenkins Global Tool confiuration' and specify that ID in tool section */
  tools {
    maven 'MAVEN_HOME'
  }
  
  //Starting of pipeline stages
  stages {
    // Scource code checkout/clone stage
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/Sinjith-Reddy/JavaWebApp.git'
      }
    }
    
    //building Java application
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
      // if build is success then the artifacts are archived
      post {
        success {
          archiveArtifacts artifacts: '**/target/*.jar'
        }
      }
    }
    
    // testing stage
    stage('Maven test') {
      steps{
        sh 'mvn test'
      }
    }
    
    //Building a docker image
    stage('Build Docker image') {
      steps {
        sh 'docker build -t sinjithreddy/javawebapp .'
      }
    }
    
    //login to dockerHub and pushing image
    stage('Login to DockerHub'{
      steps{
        sh  'echo $DockerHub_PSW | docker login -u $DockerHub_USR --password-stdin'
      }
    }
      
    stage('Push image to DockerHub'){
      steps{
        sh 'docker push sinjithreddy/javawebapp:latest'
      }
      post {
        always {
           sh 'docker logout'
        }
      }
    }
    // deploy docker image
    stage('deploy docker image') {
      steps {
        sshagent(credentials:['Credentials-ID']) {
          sh "ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_SERVER} 'docker stop javawebapp || true && docker rm javawebapp|| true'"
          sh "ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_SERVER} 'docker pull sinjithreddy/javawebapp'"
          sh "ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${REMOTE_SERVER} 'docker run --name javawebapp -dt -p 8081:8081 sinjithreddy/javawebapp:latest'"
        }
      }
    }  
  }
}
