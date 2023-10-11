pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        stage('Build image') {
            steps {
                script {
                    def app
                    app = docker.build("boukri/edureka-jenkins")
                }
            }
        }
        stage('Test image') {
            steps {
                script {
                    def app
                    app = docker.build("boukri/edureka-jenkins")
                    app.inside {
                        sh 'echo "Tests passed"'
                    }
                }
            }
        }
        stage('Push image') {
            steps {
                script {
                    def app
                    app = docker.build("boukri/edureka-jenkins")
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }

    post {
        success {
            emailext (
                to: 'boukriamine6@example.com',
                subject: "Jenkins Pipeline - Success",
                body: "The Jenkins pipeline succeeded for build ${env.BUILD_NUMBER}.",
            )
        }
        failure {
            emailext (
                to: 'boukriamine6@example.com',
                subject: "Jenkins Pipeline - Failure",
                body: "The Jenkins pipeline failed for build ${env.BUILD_NUMBER}.",
            )
        }
    }
}
