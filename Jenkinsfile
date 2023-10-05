node {

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
    script {
        def workspacePath = env.WORKSPACE.replace("\\", "/")  // Replace backslashes with forward slashes
        bat "docker run -d -t -w ${workspacePath} -v ${workspacePath}:${workspacePath} boukri/edureka echo 'Tests passed'"
    }
}


    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

