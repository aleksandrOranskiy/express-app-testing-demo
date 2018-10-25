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

    stage('Installing dependencies') {
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
  
  post {
      success {
        sh 'tar -czvf app.tar.gz app/ node_modules/ package.json > /dev/null'
      }
      
      always {
        sh 'tar -czvf test_result.tar.gz -C coverage/lcov-report/ . > /dev/null'
      }
      
      cleanup {
        archiveArtifacts artifacts: 'app.tar.gz,test_result.tar.gz', fingerprint: true
        deleteDir()
      }
  }
}
