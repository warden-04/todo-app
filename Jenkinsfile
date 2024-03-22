pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository to a specific directory
		dir('/deployment/todo-app') {
                    git branch: 'main', credentialsId: 'GitHub-Jenkins', url: 'https://github.com/warden-04/todo-app.git'
		}
            }
        }
        
	stage('Removing old Docker Container and Image') {
	    steps {
		sh '''
		   docker stop ToDoApp && docker rm ToDoApp
		   docker image rmi todo-app
		'''
	    }
	}

        stage('Build Docker Image') {
            steps {
                // Build Docker image
                sh 'docker build -t todo-app .'
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
