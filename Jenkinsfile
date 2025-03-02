pipeline {
    agent {
        docker {
            image 'node:18' 
        }
    }
    environment {
        SONAR_HOST_URL = 'http://localhost:9000'
        SONAR_TOKEN = credentials('node-token') 
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/hamza-sougou/Simple_NodeJS_App.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                sh '''
                npx sonar-scanner \
                -Dsonar.projectKey=ton-projet \
                -Dsonar.sources=. \
                -Dsonar.host.url=$SONAR_HOST_URL \
                -Dsonar.login=$SONAR_TOKEN
                '''
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ackermanon64/Simple_NodeJS_App:latest .'
            }
        }
    }
}