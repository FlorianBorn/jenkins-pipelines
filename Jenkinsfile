node {
    def hosts = readYaml file: 'hosts.yaml'
    new_active_host = [''] 
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
      environment{
        hosts2 = readYaml(file: 'hosts.yaml')
      }
      steps {
        echo "hey there!"
        host['foo'] = 'bar'
        writeYaml(file: 'host.yaml', data: host, overwrite=true)  // ['foo':'bar']
        echo(hosts2['foo'])
      }
    }

    // stage('Configure Infrastructure') {
    //   agent { label 'master'}
    //   environment {
    //       inventory_name = "inventory"
    //       playbook_name = "webserver.yaml"
    //   }
    //   steps {
    //     // Option 1 - Install Ansible Plugin and use the provided steps
    //     // Option 2 - use shell commands 
    //     dir("playbooks"){
    //         sh "ansible-playbook -i ${inventory_name} ${playbook_name}"
    //     }
    //   }
    // }    
    stage('Check HTML') {
        agent { 
          label "green-lbl"
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

    stage('Deploy on Green') {
        agent { 
          label "green-lbl"
        }      
        steps {
          
          echo 'hello from ${env.NODE_NAME}?'
          echo "hello from ${env.NODE_NAME}?"
          sh 'sudo cp website/my-website.html /var/www/html/my-website.html'
        }
    }
    stage('Test') {
        agent {
          label "green-lbl"
        }
        steps {
          sh 'curl -f http://localhost/my-website.html || exit 1'
        }
    }
    stage('Switch') {
        agent {
          label "reverse-proxy"
        }
        steps {
          input "Switch Routing / Set green to prod?" 

          sh "echo switch router"
        }
    }     
    
  }

}