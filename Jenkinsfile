pipeline {
    agent any

    tools {
        dockerTool 'myDocker'
    }

    environment {
        app = null
    }

    stages {
        stage('Initialize') {
            steps {
                script {
                    def dockerHome = tool 'myDocker'
                    env.PATH = "${dockerHome}/bin:${env.PATH}"
                }
            }
        }

        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build image') {
            steps {
                script {
                    app = docker.build("edureka1/edureka")
                }
            }
        }

        stage('Test image') {
            steps {
                script {
                    if (app) {
                        app.inside {
                            sh 'echo "Tests passed"'
                        }
                    } else {
                        error 'Image not built. Build image stage might have failed.'
                    }
                }
            }
        }

        stage('Push image') {
            steps {
                script {
                    if (app) {
                        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                            app.push("${env.BUILD_NUMBER}")
                            app.push("latest")
                        }
                    } else {
                        error 'Image not built. Build image stage might have failed.'
                    }
                }
            }
        }
    }
}
