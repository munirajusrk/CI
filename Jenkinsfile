pipeline {
    agent any

    tools {
        jdk 'java-11'
        maven 'maven'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/munirajusrk/CI.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t muniraju89docker/ci-app:1 .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop c1 || true
                docker rm c1 || true
                docker run -d --name c1 -p 8000:8080 muniraju89docker/ci-app:1
                '''
            }
        }
    }
}
