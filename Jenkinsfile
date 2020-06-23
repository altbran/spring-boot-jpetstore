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
            publishHTML([
                allowMissing: false, 
                alwaysLinkToLastBuild: false, 
                keepAll: true, 
                reportDir: 'build/reports/jacoco/test/html', 
                reportFiles: 'index.html', 
                reportName: 'JaCocoClassesReport', 
            ])
            publishHTML([
                allowMissing: false, 
                alwaysLinkToLastBuild: false, 
                keepAll: true, 
                reportDir: 'build/reports/tests/test', 
                reportFiles: 'index.html', 
                reportName: 'JaCocoTestReport', 
            ])
        }
    }

  }
}