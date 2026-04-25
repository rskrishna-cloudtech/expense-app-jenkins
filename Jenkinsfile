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
        stage('Init') {
            steps {
                sh """
                echo "Testing the jenkings pipeline"
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