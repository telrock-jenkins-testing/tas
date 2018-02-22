pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        echo "Checking out ${env.gitUrl} ${env.buildBranch}"
        git(url: env.gitUrl, branch: env.buildBranch, credentialsId: 'eaf1e289-5cdf-4aa5-8490-041fc3a27097')
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Publish jUnit tests') {
      steps {
        junit(allowEmptyResults: true, testResults: env.jUnitPattern)
      }
    }
    stage('Upload to Nexus') {
      steps {
        echo 'Loading to Nexus'
      }
    }
  }
  environment {
    gitUrl = 'https://coenie.basson@git.telrock-labs.com/telrock-spring/telrock-tas.git'
    buildBranch = 'rc/5.35.17-SNAPSHOT'
    jUnitPattern = '**/surefire-reports/*.xml'
    jBehaveReportDir = 'telrock-tas-karma/target/jbehave/view'
    jBehaveReportFiles = 'reports.html'
    jBehaveReportName = 'JBehave - Karma'
  }
}