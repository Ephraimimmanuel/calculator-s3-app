pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Clean') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Ephraimimmanuel/calculator-s3-app.git'
            }
        }

        stage('Deploy to S3') {
            steps {
                bat '''
                aws s3 sync . s3://calculator-devops-app --delete
                '''
            }
        }
    }
}