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
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
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
    stage('Rolling Deployment') {
      steps {
        withAWS(region:'us-east-2', credentials:'aws-master') {
          sh 'kubectl apply -f ./deployment/deployments.yml --record=true'
          sh 'kubectl rollout status deployment nodeapp'
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
