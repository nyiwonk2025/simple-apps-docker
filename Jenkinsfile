pipeline {
    agent {
        label 'devops2'
        }

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/nyiwonk2025/simple-apps-docker.git'
            }
        }
        stage('Build') {
            steps {
                sh '''cd apps
                npm install'''
            }
        }
        stage('Testing') {
            steps {
                sh '''cd apps
                npm test
                npm run test:coverage'''
            }
        }
        stage('Code Review') {
            steps {
                sh '''cd apps
                sonar-scanner \
                -Dsonar.projectKey=Test-Apps \
                -Dsonar.sources=. \
                -Dsonar.host.url=172.23.13.112:9000  \
                -Dsonar.login=sqp_90f8c3486d5e4104f643ed6d636ca2ac50571239 '''
            }
        }
        stage('Deploy compose') {
            steps {
                sh '''
                docker compose build
                docker compose up -d
                '''
            }
        }
    }
}