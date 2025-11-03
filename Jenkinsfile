pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Ezekiel-redhat/Birkenstock.git'
            }
        }
 
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t birkenstock-app .'
            }
        }
 
        stage('Scan Image with Trivy') {
            steps {
                sh 'trivy image birkenstock-app || true'
            }
        }
 
        stage('Deploy Container') {
            steps {
                sh '''
                    docker stop birkenstock-app || true
                    docker rm birkenstock-app || true
                    docker run -d -p 5000:5000 --name birkenstock-app birkenstock-app
                '''
            }
        }
    }
}
