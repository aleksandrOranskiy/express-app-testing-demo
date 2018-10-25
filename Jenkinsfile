pipeline {
  agent {
      node {
          label 'jenkins_slave'
      }
  }

  tools {nodejs "NodeJS11.0.0"}

  stages {
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
    
    stage('Starting an app') {
      steps {
        sh 'npm start' 
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
      }
  }
}
