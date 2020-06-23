pipeline {
   agent any
   stages {
    stage('Checkout') {
        steps {
           git credentialsId: 'jenkins-user-github', url: 'https://github.com/altbran/spring-boot-jpetstore.git'
        }
    }
    stage('Build') {
        steps {
            sh './gradlew build jacocoTestReport'
        }
    }

    stage('Test') {
      steps {
        sh './gradlew clean test'
      }
    }
    stage('Analyze') {
        steps {
            sh './gradlew sonarqube -Dsonar.host.url=http://sonarqube:9000'
        }
    }
   }
}
