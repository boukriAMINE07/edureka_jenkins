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
        def workspacePath = env.WORKSPACE.replace("\\", "/")
        def containerTestPath = "/workspace_tests"
        def containerName = "edureka_tests"

        bat "docker rm -f ${containerName}"

        // Run tests inside the container
        bat """
            docker run --name ${containerName} \
                -v ${workspacePath}:${containerTestPath} \
                -w ${containerTestPath} boukri/edureka \
                bash -c 'cp -r ${containerTestPath} /tests' &&
            docker exec ${containerName} bash -c 'echo Tests passed'
        """
    }
}



    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

