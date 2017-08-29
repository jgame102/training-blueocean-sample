pipeline {
  agent {
    docker {
      args '-u root -v $HOME/.m2:/root/.m2'
      image 'bitwiseman/training-blueocean-sample'
    }
    
  }
  stages {
    stage('Build') {
      steps {
        sh './jenkins/build.sh'
        archiveArtifacts(artifacts: 'target/*.war', allowEmptyArchive: true)
      }
    }
    stage('Test') {
      steps {
        parallel(
          "Test": {
            sh './jenkins/test-all.sh'
            junit ' **/surefire-reports/**/*.xml'
            junit '**/test-results/karma/*.xm'
            
          },
          "Frontend": {
            sh '''./jenkins/test-frontend.sh



'''
            
          },
          "Report": {
            junit ' **/test-results/karma/*.xml'
            
          },
          "Backend": {
            sh '''./jenkins/test-backend.sh




'''
            
          },
          "Static": {
            sh '''./jenkins/test-static.sh



'''
            
          }
        )
      }
    }
  }
}