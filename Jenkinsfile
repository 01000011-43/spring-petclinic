node {
  stage('SCM') {
    checkout scm
  }
  
  stage('Build JAR') {
    def mvn = tool 'maven';
    sh "${mvn}/bin/mvn clean install"
  }

  stage('Run JAR') {
    steps {
      // Replace '/path/to/spring-petclinic-3.1.0-SNAPSHOT.jar' with the actual path
      // to your JAR file in the Jenkins workspace
      sh 'java -jar target/spring-petclinic-3.1.0-SNAPSHOT.jar --port=8888'
    }
  }
  
  stage('SonarQube Analysis') {
    def mvn = tool 'maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn sonar:sonar -Dsonar.projectKey=devopsProject -Dsonar.projectName='devopsProject'"
    }
  }
}

