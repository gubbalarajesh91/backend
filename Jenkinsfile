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
    
    
    // stage('Nexus Artifact Upload'){
    //         steps{
    //             script{
    //                 nexusArtifactUploader(
    //                     nexusVersion: 'nexus3',
    //                     protocol: 'http',
    //                     nexusUrl: "${nexusUrl}",
    //                     groupId: 'com.expense',
    //                     version: "${appVersion}",
    //                     repository: "backend",
    //                     credentialsId: 'nexus-auth',
    //                     artifacts: [
    //                         [artifactId: "backend" ,
    //                         classifier: '',
    //                         file: "backend-" + "${appVersion}" + '.zip',
    //                         type: 'zip']
    //                 ]
    //             )
    //         }
    //     }
    // }

        stage('Deploy'){
            steps{
                script{
                    def params = [
                        string(name: 'appVersion', value: "${appVersion}")
                    ]
                    build job: 'backend-deploy', parameters: params, wait: false
                }
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
