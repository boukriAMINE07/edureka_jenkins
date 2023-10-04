pipeline {
    agent any

    stages {
        stage('Check Docker Version') {
            steps {
                script {
                    def dockerPath = "\"/c/Program Files/Docker/Docker/resources/bin/docker\""
                    sh "${dockerPath} --version"
                }
            }
        }
    }
}
