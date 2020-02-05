pipeline {
  agent {
    label 'master'
  }
  stages {
    stage('Example') {
      steps {
        echo 'Hello World'
      }
    }

    stage('Green') {
      agent {
        label 'green-lbl'
      }
      steps {
        echo 'hello from green?'
        sh 'ls'
        sh 'cp website/my-website.html /var/www/html/my-website.html'
      }
    }

  }
}