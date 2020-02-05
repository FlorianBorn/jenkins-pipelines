pipeline {
  agent {
    label 'master'
  }
  environment {
      ACTIVE_HOST = "${cat 'active-server.txt'}"
      IDLE_HOST = "${cat 'idle-server.txt'}"
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
        sh 'cat active-server.txt'
      }
    }
    stage('Blue') {
        when {
            beforeAgent true
            equals expected: IDLE_HOST, actual: ACTIVE_HOST
        }
        sh echo 'Im Blue!'
        sh echo 'active host: ${ACTIVE_HOST}'
        sh echo 'idle host: ${IDLE_HOST}'
    }

  }
  environment {
    active_host = 'green'
  }
}