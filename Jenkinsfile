pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository into a specific directory
                dir('/deployment') {
                    git 'https://github.com/warden-04/todo-app.git'
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Build Docker image
                script {
                    docker.build('todo-app:latest')
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                // Run Docker container
                script {
                    docker.image('todo-app:latest').run('-p 3020:3020', '--name ToDoApp')
                }
            }
        }
    }
}
