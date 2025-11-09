pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/SowmyaVasudevan/Project-1.git'
            }
        }

        stage('Build Static Website') {
            steps {
                echo 'Building React app...'
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Deploy to S3') {
            steps {
                withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                    sh 'aws s3 sync build/ s3://my-static-website-bucket --delete'
                }
            }
        }
    }
}
