pipeline {
    agent {
        label 'AGENT-1'
    }

    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }

    // Declaring a global variable appVersion.
    environment{
        def appVersion = ''
    }

    stages {
        stage ('Read the Application Version') {
            steps {
                // Grrovy script to create the variables.
                script {
                    // Will store the entire package.json file into packageJSON variable.
                    def packageJSON = readJSON file: 'package.json'
                    // Take the value of version from the packageJSON and store into the appVersion variable.
                    appVersion = packageJSON.version
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh """
                npm install
                """
            }
        }

        stage('Build') {
            steps {
                sh """
                // It will zip all the files and directories from the project folder excep Jenkinsfile and a .zip if of the project if there are any.
                zip -q -r backend-${appVersion}.zip * -x Jenkinsfile -x backend-${appVersion}.zip
                ls -ltr
                """
            }
        }
    }

    post{
        always{
            deleteDir()
        }
    }
}