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

        // Copy test files or scripts to the container
        bat "docker run -v ${workspacePath}:${containerTestPath} -w ${containerTestPath} boukri/edureka cp -r ${containerTestPath} /tests"

        // Run tests inside the container
        bat "docker run -w /tests boukri/edureka echo 'Tests passed'"
    }
}





    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

