pipeline {
  agent any

  environment {
    IMAGE_NAME = "basil-backend"
    ECR_REPO = "182399722085.dkr.ecr.us-east-1.amazonaws.com/basil-backend"
  }

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/muratkocer6/basilbartending.git', branch: 'main'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $IMAGE_NAME .'
      }
    }

    stage('Login to ECR') {
      steps {
        sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin $ECR_REPO'
      }
    }

    stage('Push to ECR') {
      steps {
        sh 'docker tag $IMAGE_NAME $ECR_REPO'
        sh 'docker push $ECR_REPO'
      }
    }
  }
}
