pipeline {
    agent {
        label 'AGENT-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    environment{
        def appVersion = '' //variable declaration
    }
    stages {
        stage('read the version') {
            steps {
                script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version                        //variable assigned
                    echo "Application version is $appVersion"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh """
                npm install
                ls -ltr
                echo "Application version is $appVersion"
                """
            }
        }
        stage('Build'){
            steps{
                sh """
                zip -q -r backend-${appVersion}.zip * -x Jenkinsfile -x backend-${appVersion}.zip
                ls -ltr
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
