pipeline {
    agent {label 'master'}
    stages { 
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Green') {
            agent { label 'green-lbl' }
            steps {
                echo 'hello from green?'
                sh "ls"
            }
        }
    }
}
