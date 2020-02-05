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
      environment {
        active_server = 'green'
      }
      steps {
        echo 'hello from green?'
        sh 'ls'
        sh 'whoami'
        sh 'sudo cp website/my-website.html /var/www/html/my-website.html'
        sh 'echo ${active_host}'
        sh 'cat active-host.txt'
      }
    }

  }
  environment {
    active_host = 'green'
  }
}