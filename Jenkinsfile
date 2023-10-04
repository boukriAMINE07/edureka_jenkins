node {

    agent {
        docker {
            image 'boukri/edureka'
            args '-v C:/ProgramData/Jenkins/.jenkins/workspace/edureka:/workspace -w /workspace'
        }
    }
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        echo "start build image"
        app = docker.build("boukri/edureka")
        echo "end build image"
    }

    stage('Test image') {
        app.inside {
            echo "Tests passed"
        }
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
