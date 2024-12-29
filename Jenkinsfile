pipeline {
    agent any
    
    stages {
        stage ("Checkout") {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/karthik-storage/Jenkins-Java-App.git']])
            }
        }
        stage ("Tool Version Check") {
            steps {
                sh "java --version"
                sh "mvn --version"
            }
        }
        
        stage ("Build") {
            steps {
                sh returnStdout: true, script: 'mvn clean install -DskipTests'
            }
        }
    }
    post {
        always {
            cleanWs(cleanWhenNotBuilt: true,
                    deleteDirs: true,
                    disableDeferredWipeout: true,
                    notFailBuild: true,
                    patterns: [[pattern: 'target/', type: 'INCLUDE']])
        }
    }
}