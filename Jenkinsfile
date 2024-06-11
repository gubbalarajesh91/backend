pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }

    stages {
        stage('Test') {
            steps {
                sh """
                echo " this is test"
                """
            }
        }

    }
    post {
        always{
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success {
            echo "run when pipeline is success"
        }
        failure {
            echo 'This will run when pipeline is failed'
        }
    }
}