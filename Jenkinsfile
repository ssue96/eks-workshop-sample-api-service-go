pipeline {
  agent any
  stages {
    stage('ready') {
      steps {
        git(url: 'https://github.com/ssue96/eks-workshop-sample-api-service-go.git', branch: 'master', credentialsId: 'a0bb03f6-d72f-4498-b2df-09669e1feb61')
        sh '''sh """
pwd
"""

'''
      }
    }

    stage('build') {
      steps {
        sh '''sh """
docker build -t eks-workshop .
"""'''
      }
    }

    stage('push') {
      steps {
        sh '''sh """
$(aws ecr get-login --no-include-email --region ap-northeast-2)
docker tag eks-workshop:latest 536983495792.dkr.ecr.ap-northeast-2.amazonaws.com/eks-workshop:latest
docker push 536983495792.dkr.ecr.ap-northeast-2.amazonaws.com/eks-workshop:latest
"""'''
      }
    }

    stage('deploy') {
      steps {
        sh '''sh """
kubectl apply -f hello-k8s.yml
"""'''
      }
    }

  }
}