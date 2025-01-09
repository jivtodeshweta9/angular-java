pipeline {
    agent any

    environment {
        FRONTEND_DIR = 'frontend'
        BACKEND_DIR = 'backend'
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository
                git url: 'https://github.com/cloud-blitz/angular-java.git', branch: 'main'
            }
        }

        stage('Install Frontend Dependencies') {
            steps {
                dir(FRONTEND_DIR) {
                    script {
                        // Install Node.js dependencies for the Angular project
                        sh 'npm install'
                    }
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir(FRONTEND_DIR) {
                    script {
                        // Build the Angular project
                        sh 'npm run build'
                    }
                }
            }
        }

        stage('Build Backend') {
            steps {
                dir(BACKEND_DIR) {
                    script {
                        // Build the Java backend using Maven
                        sh 'mvn clean package'
                    }
                }
            }
        }

        stage('Deploy Backend') {
            steps {
                dir(BACKEND_DIR) {
                    script {
                        // Run the Spring Boot application
                        sh 'java -jar target/*.jar'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution finished.'
        }
        success {
            echo 'Build and deployment completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs for errors.'
        }
    }
}
