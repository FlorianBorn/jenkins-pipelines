pipeline {
  environment {
    ACTIVE_HOST = sh "cat active-server.txt"
    IDLE_HOST = sh "cat idle-server.txt"
  }
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
        sh 'cat active-server.txt'
      }
    }
    stage('Blue') {
        when {
            beforeAgent true
            equals expected: IDLE_HOST, actual: ACTIVE_HOST
        }
        steps {
            echo 'Im Blue!'
            //echo 'active host: ${ACTIVE_HOST}'
            echo 'active host: $ACTIVE_HOST'
            echo 'idle host: $IDLE_HOST'
        }

    }

  }

}