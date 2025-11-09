pipeline {
  agent any

  environment {
    BUCKET = "my-react-static-site"   // 🪣 Replace with your actual S3 bucket name
    REGION = "us-east-1"              // 🗺️ Replace with your AWS region
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/SowmyaVasudevan/Project-1.git'
      }
    }

    stage('Deploy to S3') {
      steps {
        withCredentials([[
          $class: 'AmazonWebServicesCredentialsBinding',
          credentialsId: 'aws-jenkins-creds',
          accessKeyVariable: 'AWS_ACCESS_KEY_ID',
          secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
        ]]) {
          sh '''
            aws configure set default.region ${REGION}
            aws s3 sync build/ s3://${BUCKET} --delete --acl public-read
            aws s3 website s3://${BUCKET} --index-document index.html --error-document index.html
          '''
        }
      }
    }
  }
}
