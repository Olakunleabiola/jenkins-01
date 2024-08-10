pipeline {
  agent any
  tools {
    maven 'maven'
  }
  stages{
    stage('1-git-clone'){
      steps{
        checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/Olakunleabiola/jenkins-01.git']])
    }
    stage('2-cleanws'){
      steps{
        sh 'mvn clean'
      }
    }
    stage('3-mavenbuild'){
      steps{
        sh 'mvn package'
      }
    }
    stage('unittest'){
        steps{
            sh 'mvn test'
        }
    }
    stage('codequality'){
        steps{
       sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=team10 \
  -Dsonar.host.url=http://35.94.178.191:9000 \
  -Dsonar.login=sqp_05e2a16f75885c94d1efa6fd2630a02f12a46f9a"
      }
    }
stage('5-deploy-to-tomcat') {
    steps {
        sshagent(['tomcat']) {
          sh """
         scp -o StrictHostKeyChecking=no ~/workspace/maven-build/MavenEnterpriseApp-web/target/MavenEnterpriseApplication.war ubuntu@34.209.53.251:/opt/tomcat/apache-tomcat-9.0.93/webapps
          """           
            }
        }
    }
}

     