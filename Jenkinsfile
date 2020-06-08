pipeline {
  agent any
  stages {
    stage('Lint HTML') {
      steps {
        sh 'echo "Verify all html files."'
        sh 'tidy -q -e *.html'
      }
    }    
  }
}
