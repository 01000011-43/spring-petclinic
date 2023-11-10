node {
  stage('SCM') {
    checkout scm
  }
  
  stage('Build JAR') {
    def mvn = tool 'maven';
    sh "${mvn}/bin/mvn clean install"
  }
  
  stage('SonarQube Analysis') {
    def mvn = tool 'maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn sonar:sonar -Dsonar.projectKey=devopsProject -Dsonar.projectName='devopsProject'"
    }
  }
}

