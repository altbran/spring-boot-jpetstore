pipeline {
  agent any
  stages {
    stage('Build') {
      agent any
      steps {
        sh './gradlew build'
      }
    }

    stage('Test') {
      steps {
        sh './gradlew clean test'
      }
    }

    stage('Jacoco Results') {
      steps {
        sh './gradlew -i test jacocoTestReport'
      }
    }

    stage('Analyze') {
      steps {
        sh './gradlew sonarqube -Dsonar.host.url=http://192.168.1.108:9000'
      }
    }

    stage('Report') {
      steps {
        sh 'echo "JACOCO tests report: ${BUILD_URL}build/reports/jacoco/test/html/index.html"'
      }
    }

  }
}