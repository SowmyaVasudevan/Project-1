pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/SowmyaVasudevan/Project-1.git'
            }
        }

        stage('Deploy to S3') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-s3-deploy']]) {
                    sh '''
                        echo "Setting AWS region..."
                        aws configure set default.region us-east-1
                        
                        echo "Deploying static site to S3..."
                        aws s3 sync build/ s3://app1-payments-prod-example2.com --delete
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "Deployment successful! Static website uploaded to S3."
        }
        failure {
            echo "Deployment failed. Check AWS credentials, bucket policy, or folder path."
        }
    }
}
