pipeline {
    agent any
    tools {
        maven 'maven' // Make sure 'maven' is configured in Jenkins Global Tool Configuration
    }
    stages {
        stage('1 - Cloning Project Repo') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']], 
                    extensions: [], 
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/Olakunleabiola/jenkins-01.git']])
                )
            }
        }
        stage('2 - Clean Workspace') {
            steps {
                cleanWs() // Cleans up the workspace before starting the build
            }
        }
        stage('3 - Maven Build') {
            steps {
                sh 'mvn clean package' // Combining clean and package
            }
        }
    }
    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Please check the logs for details.'
        }
    }
}
