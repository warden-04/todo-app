pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from GitHub repository
                    git branch: 'main', credentialsId: 'GitHub-Jenkins', url: 'https://github.com/warden-04/todo-app.git'
            }
        }

	stage('Delete Old Docker Container and Image') {
            steps {
                script {
                    // Check if the specific container exists
                    def containerId = sh(script: "docker ps -aqf name=ToDoApp", returnStdout: true).trim()
                    // Check if the specific image exists
                    def imageId = sh(script: "docker images -q todo-app", returnStdout: true).trim()

                    if (containerId && imageId) {
                        // Delete the specific container
			sh "docker stop $containerId || true"
                        sh "docker rm $containerId || true"
                        // Delete the specific image
                        sh "docker rmi $imageId || true"
                    } else {
                        echo 'No old container or image found'
                    }
                }
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
