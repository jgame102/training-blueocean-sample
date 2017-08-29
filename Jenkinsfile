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
        sh './jenkins/test-all.sh'
        junit ' **/surefire-reports/**/*.xml'
      }
    }
  }
}