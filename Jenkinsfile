pipeline {
  agent any

  environment {
    AWS_REGION = 'ap-south-1'
    ECR_URL = '819439780835.dkr.ecr.ap-south-1.amazonaws.com'
  }

  stages {

    stage('Clone Code') {
        steps {
            git branch: 'main', url: 'https://github.com/rajkumaramithn/MERNwithMicroservices.git'
  }
}

    stage('Test') {
      steps {
        echo 'Jenkins pipeline is working 🚀'
      }
    }

    stage('Build Backend Image') {
      steps {
        sh 'docker build -t backend ./backend'
      }
    }

    stage('Build Frontend Image') {
      steps {
        sh 'docker build -t frontend ./frontend'
      }
    }

    stage('Login to ECR') {
      steps {
        sh '''
        aws ecr get-login-password --region $AWS_REGION | \
        docker login --username AWS --password-stdin $ECR_URL
        '''
      }
    }

    stage('Push Backend') {
      steps {
        sh '''
        docker tag backend:latest $ECR_URL/backend:latest
        docker push $ECR_URL/backend:latest
        '''
      }
    }

    stage('Push Frontend') {
      steps {
        sh '''
        docker tag frontend:latest $ECR_URL/frontend:latest
        docker push $ECR_URL/frontend:latest
        '''
      }
    }
  }
}