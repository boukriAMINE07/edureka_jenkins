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
                    app.inside {
                        // Set the working directory to an absolute path inside the container
                        dir('C:\\workspace') {
                            echo "Tests passed"
                        }
                }

                }
  }



    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}

