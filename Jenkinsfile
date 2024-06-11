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
        stage('read the version') {
            steps {
                def packageJson = readJSON file: 'package.json'
                def appVesrion = packageJson.version

            }
        }
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh """
                npm install
                ls -ltr
                echo $appVesrion

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