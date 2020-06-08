pipeline {
  environment {
    registry = "ctanlcs/eks-docker-hub"
    registryCredential = 'eks-docker-hub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Lint HTML') {
      steps {
        sh 'echo "Verify all html files."'
        sh 'tidy -q -e *.html'
      }
    }
    stage('Building image') {
      steps {
        script {
          dockerImage = docker.build registry + ":BUILD_NUMBER"
        }
      }
    }
    stage('Deploy Image') {
      steps {
        script {
          docker.withRegistry('', registryCredential) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps {
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }    
  }
}
