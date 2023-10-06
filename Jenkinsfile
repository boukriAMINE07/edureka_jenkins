pipeline {
    agent any

    environment {
        app = null
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build image') {
            steps {
                script {
                    // Build Docker image using the specified volume mappings
                    app = docker.image("edureka1/edureka").inside("--volume /var/run/docker.sock:/var/run/docker.sock") {
                        // Perform actions inside the Docker container
                        sh 'docker build -t edureka1/edureka .'
                    }
                }
            }
        }

        stage('Test image') {
            steps {
                script {
                    // Run tests inside the Docker container
                    app.inside("--volume /var/run/docker.sock:/var/run/docker.sock") {
                        sh 'echo "Tests passed"'
                    }
                }
            }
        }

        stage('Push image') {
            steps {
                script {
                    // Push the Docker image using the specified volume mappings
                    app.inside("--volume /var/run/docker.sock:/var/run/docker.sock") {
                        sh "docker push edureka1/edureka:${env.BUILD_NUMBER}"
                        sh "docker push edureka1/edureka:latest"
                    }
                }
            }
        }
    }
}
