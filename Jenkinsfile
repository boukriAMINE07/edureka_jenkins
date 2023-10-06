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

      
    }
}
