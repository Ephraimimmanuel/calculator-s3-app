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
        stage('Test AWS Login') {
    steps {
        withCredentials([
            [$class: 'AmazonWebServicesCredentialsBinding',
             credentialsId: 'AKIA4YV46Q4GWBXN6MWP']
        ]) {
            bat 'aws sts get-caller-identity'
        }
    }
}
        

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Ephraimimmanuel/calculator-s3-app.git'
            }
        }
        stage('Check AWS') {
            steps {
                bat 'aws --version'
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