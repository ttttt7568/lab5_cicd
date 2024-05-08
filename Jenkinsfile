pipeline {
    agent any
    
    tools {
        gradle '8.7'
    }
    stages {
        stage('Build') {
            steps {
                // Run Gradle build
                sh 'gradle build'
                sh 'build/libs/hello.jar > output.log'
            }
        }
    }
    post {
        success {
            // Archive and attach JAR file
            archiveArtifacts artifacts: 'build/libs/hello.jar', fingerprint: true
            // Create tarball and rename it
            sh "tar -czf hello-\${BUILD_NUMBER}.tar.gz build/libs/hello.jar"
            // Attach the tarball
            archiveArtifacts artifacts: "hello-\${BUILD_NUMBER}.tar.gz", fingerprint: true
            // Attach output.log file
            archiveArtifacts artifacts: 'output.log', fingerprint: true
        }
    }
}
