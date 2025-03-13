pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/KunjPatel116/my-webapp.git', branch: 'main'
            }
        }
        stage('Build Maven Project') {
            steps {
                bat 'mvn clean package'
            }
        }
        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    bat 'echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin'
                }
            }
        }
        stage('Docker Build') {
            steps {
                bat 'docker build -t kunj116/my-webapp:latest .'
            }
        }
        stage('Docker Push') {
            steps {
                bat 'docker push kunj116/my-webapp:latest'
            }
        }
    }
}