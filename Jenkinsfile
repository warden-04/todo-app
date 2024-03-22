pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository
                    git branch: 'main', credentialsId: 'GitHub-Jenkins', url: 'https://github.com/warden-04/todo-app.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Build Docker image
                sh 'docker build -t node-app .'
            }
        }
        
        stage('Run Docker Container') {
            steps {
                // Run Docker container
                sh 'docker run -d --name ToDoApp -p 3020:3020 todo-app'
            }
        }
    }
}
