pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Ephraimimmanuel/calculator-s3-app.git'
            }
        }

        stage('Check AWS CLI') {
            steps {
                bat 'aws --version'
            }
        }

        stage('Verify AWS Login') {
            steps {
                withCredentials([
                    [$class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-s3-cred']
                ]) {
                    bat 'aws sts get-caller-identity'
                }
            }
        }

        stage('Deploy to S3') {
            steps {
                withCredentials([
                    [$class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-s3-cred']
                ]) {
                    bat 'aws s3 sync . s3://calculator-devops-app --delete'
                }
            }
        }

    }

    post {
        success {
            echo 'Deployment to S3 completed successfully.'
        }

        failure {
            echo 'Deployment failed. Check console logs.'
        }
    }
}