pipeline {
  agent {
      node {
          label 'jenkins_slave'
      }
  }
    
  tools {nodejs "NodeJS11.0.0"}
    
  stages {
    stage('Cloning Git') {
      steps {
        git credentialsId: '53f2975c-026e-4327-bb11-224c8b4602ab', url: 'git@github.com:aleksandrOranskiy/express-app-testing-demo.git'
      }
    }
        
    stage('Install dependencies') {
      steps {
        sh 'npm install'
      }
    }
     
    stage('Unit and integration tests') {
      steps {
         sh 'npm test'
      }
    }
  }
}
