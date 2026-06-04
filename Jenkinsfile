pipeline {
    agent any

    environment {
        BUCKET = "calculator-devops-app"
    }

    stages {

        stage('Clone Repo') {
            steps {
                git 'https://github.com/Ephraimimmanuel/calculator-s3-app.git'
            }
        }

        stage('Deploy to S3') {
            steps {
                sh '''
                aws s3 sync . s3://$BUCKET --delete
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment SUCCESS 🚀"
        }
        failure {
            echo "Deployment FAILED ❌"
        }
    }
}