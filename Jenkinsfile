pipeline {
  agent {
    docker {
      args '-u root -v $HOME/.m2:/root/.m2'
      image 'bitwiseman/training-blueocean-sample'
    }
    
  }
  stages {
    stage('Hello') {
      steps {
        sh '''echo Hello word!!!
'''
      }
    }
  }
}