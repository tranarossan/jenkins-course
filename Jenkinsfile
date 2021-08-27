pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        git(url: 'https://github.com/axel-sirota/jenkins-course/', branch: 'main', poll: true)
        sh 'mvn -f maven-static-code-analysis clean compile'
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            sh 'mvn -f maven-static-code-analysis clean test'
          }
        }

        stage('Static checker') {
          steps {
            sh 'mvn -f maven-static-code-analysis site'
          }
        }

      }
    }

    stage('Report') {
      steps {
        recordIssues()
      }
    }

  }
}