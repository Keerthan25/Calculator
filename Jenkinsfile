pipeline {
  agent any
 stages {
  stage('SCM') {
    steps {
    checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Keerthan25/Calculator.git']])
  }
  }
  stage('SonarQube Analysis') {
    steps {
    def mvn = tool 'Default Maven';
    withSonarQubeEnv(instalationName: 'sonar') {
      sh "${mvn}/bin/mvn clean test sonar:sonar -Dsonar.projectKey=jenkins"
    }
  }
 }
  stage('Quality Gate') {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }        
}
