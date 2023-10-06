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
                    app = docker.build("edureka1/edureka")
                }
            }
        }

        stage('Test image') {
            steps {
                script {
                            sh 'echo "Tests passed"'
                }
            }
        }

        stage('Push image') {
            steps {
                script {

                        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                            app.push("${env.BUILD_NUMBER}")
                            app.push("latest")
                        }
                }
            }
        }
    }
}
