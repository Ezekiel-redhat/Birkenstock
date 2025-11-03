pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                echo 'Pulling latest code from GitHub...'
                checkout scm
            }
        }
 
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t birkenstock-app .'
            }
        }
 
        stage('Security Scan with Trivy') {
            steps {
                echo 'Running Trivy scan...'
                sh 'trivy image birkenstock-app || true'
            }
        }
 
        stage('Run Container') {
            steps {
                echo 'Running container...'
                sh 'docker run -d -p 5000:5000 birkenstock-app'
            }
        }
    }
    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
        failure {
            echo 'Pipeline failed 🚨'
        }
    }
}
