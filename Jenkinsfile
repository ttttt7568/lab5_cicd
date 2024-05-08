pipeline {
    agent any
    
    tools {
        gradle '8.7'
    }
    stages {
        stage('Build') {
            steps {
                sh 'gradle build'
                sh 'java -jar build/libs/hello.jar > output.log'
            }
        }
        stage('Make archive') {
            steps {
                sh 'tar -czf hello-${BUILD_NUMBER}.tar.gz build/libs/hello.jar output.log'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: "hello-${BUILD_NUMBER}.tar.gz", fingerprint: true
        }
    }
}
