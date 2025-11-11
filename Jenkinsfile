pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-1'    
        S3_BUCKET = 'app1-payments-prod-example2.com'   
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/SowmyaVasudevan/Project-1.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy to S3') {
            steps {
                withAWS(credentials: 'aws-s3-deploy', region: "${AWS_REGION}") {
                    sh 'aws s3 sync build/ s3://${S3_BUCKET} --delete --acl public-read'
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment successful! Your app is live on S3.'
        }
        failure {
            echo 'Deployment failed. Check AWS credentials or S3 bucket permissions.'
        }
    }
}
