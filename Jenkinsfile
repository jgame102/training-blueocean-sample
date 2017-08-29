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
          "Frontend": {
            sh '''./jenkins/test-frontend.sh



'''
            
          },
          "Backend": {
            sh '''./jenkins/test-backend.sh




'''
            
          },
          "Static": {
            sh '''./jenkins/test-static.sh



'''
            
          },
          "Performance": {
            sh '''./jenkins/test-performance.sh



'''
            
          }
        )
      }
    }
    stage('Deploy to Dev') {
      steps {
        sh './jenkins/deploy.sh dev'
      }
    }
  }
}