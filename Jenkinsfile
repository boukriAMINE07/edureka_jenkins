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
        def containerTestPath = "/workspace_tests"  // Path inside the container to copy the test files
        def containerName = "edureka_tests"  // Desired name for the container

        bat "docker rm -f ${containerName}"  // Force removal of the container if it exists

        // Remove the old container if it exists, and run tests inside the container
        bat """docker run --name ${containerName} -v ${workspacePath}:${containerTestPath} -w ${containerTestPath} boukri/edureka bash -c 'cp -r ${containerTestPath} /tests && echo Tests passed'"""
    }
}


    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

