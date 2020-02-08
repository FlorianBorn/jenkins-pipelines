node {
    hosts = readYaml file: 'hosts.yaml'
}

pipeline {
  agent {
    label 'master'
  }
  stages {
// Configure Infrastructure
// run Ansible to set up the TARGET infrastructure (reverse-proxy, green, blue)

// Test
// test HTML with tidy

// ggf. manuell input (approve deployment to production)

// Deploy

    stage('Example') {
      steps {
        echo "${hosts.idle_host}"
      }
    }

    stage('Configure Infrastructure') {
      agent { label 'master'}
      environment {
          inventory_name = "inventory"
          playbook_name = "webserver.yaml"
      }
      steps {
        // Option 1 - Install Ansible Plugin and use the provided steps
        // Option 2 - use shell commands 
        dir("playbooks"){
            sh "ansible-playbook -i ${inventory_name} ${playbook_name}"
        }
      }
    }    
    stage('Check HTML') {
        agent { 
          label "${hosts.idle_host}-lbl"
        }
        environment {
            html_dir = "website/"
        }
        steps {
            dir(html_dir) {
                sh "tidy my-website.html"
            }
        }
    }

    stage('Deploy on Idle Server') {
        agent { 
          label "${hosts.idle_host}-lbl"
        }      
        steps {
          
          echo 'hello from ${env.NODE_NAME}?'
          echo "hello from ${env.NODE_NAME}?"
          sh 'sudo cp website/my-website.html /var/www/html/my-website.html'
          // copy("website/my-website.html", "/var/www/html/")
          // sh 'printenv | sort'           
          // sh 'ls'
          // sh 'whoami'

        }
    }
    // stage('Test') {

    // }        
    

//     stage('Deploy Green') {
//       agent {
//         label 'green-lbl'
//       }
//       when {
//         beforeAgent true
//         equals expected: 'green', actual: "${hosts.active_host}"
//       }
//     //   environment {
//     //     active_server = 'green'
//     //   }
//       steps {
//         sh 'printenv | sort'  
//         echo 'hello from ${env.NODE_NAME}?'
//         echo "hello from ${env.NODE_NAME}?"
//         sh 'ls'
//         sh 'whoami'
//         sh 'sudo cp website/my-website.html /var/www/html/my-website.html'
// //        sh 'echo ${active_host}'
//         sh 'cat active-server.txt'
//       }
//     }

//     stage('Deploy Blue') {
//       agent {
//         label 'blue-lbl'
//       }
//       when {
//         beforeAgent true
//         equals expected: 'blue', actual: "${hosts.active_host}"
//       }

//       steps {
//         echo 'Im Blue!'
//         sh 'printenv | sort'
//         echo 'active host: $ACTIVE_HOST'
//         echo 'idle host: $IDLE_HOST'
//       }
//     }

//     stage('switch') {
//         steps {
//             echo "hi i'm switch!"
//         }
//     }

  }
//   environment {
//     ACTIVE_HOST = 'cat active-server.txt'
//     IDLE_HOST = 'cat idle-server.txt'
//   }
}