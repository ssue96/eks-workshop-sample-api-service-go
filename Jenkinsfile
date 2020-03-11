pipeline {
  agent any
  stages {
    stage('ready') {
      steps {
        git(url: 'https://github.com/ssue96/eks-workshop-sample-api-service-go.git', branch: 'master', credentialsId: 'a0bb03f6-d72f-4498-b2df-09669e1feb61')
      }
    }

    stage('build') {
      steps {
        echo '"build test"'
      }
    }

    stage('push') {
      steps {
        echo '"push test"'
      }
    }

    stage('deploy') {
      steps {
        echo '"deploy test"'
      }
    }

  }
}