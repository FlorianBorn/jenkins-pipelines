node {
    hosts = readYaml file: 'hosts.yaml'
}

pipeline {
  agent {
    label 'master'
  }
  stages {
    stage('Example') {
      steps {
        echo 'Hello World'
        //readFile 'active-server.txt'
        echo "${hosts.idle_host}"
        sh 'printenv | sort'
      }
    }

    stage('Green') {
      agent {
        label 'green-lbl'
      }
      when {
        beforeAgent true
        equals expected: 'green', actual: "${hosts.active_host}"
      }
    //   environment {
    //     active_server = 'green'
    //   }
      steps {
        echo 'hello from ${env.NODE_NAME}?'
        sh 'ls'
        sh 'whoami'
        sh 'sudo cp website/my-website.html /var/www/html/my-website.html'
//        sh 'echo ${active_host}'
        sh 'cat active-server.txt'
      }
    }

    stage('Blue') {
      agent {
        label 'blue-lbl'
      }
      when {
        beforeAgent true
        equals expected: 'blue', actual: "${hosts.active_host}"
      }

      steps {
        echo 'Im Blue!'
        sh 'printenv | sort'
        echo 'active host: $ACTIVE_HOST'
        echo 'idle host: $IDLE_HOST'
      }
    }

  }
//   environment {
//     ACTIVE_HOST = 'cat active-server.txt'
//     IDLE_HOST = 'cat idle-server.txt'
//   }
}