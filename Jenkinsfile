pipeline {
    agent any

    environment {
        dockerImage = ''
    }

    stages {
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("$MY_DOCKER_REGISTRY_URL/sampledotnetcorewebapp:$BUILD_NUMBER", "-f SampleDotNetCoreWebApp/Dockerfile .")
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry("http://$MY_DOCKER_REGISTRY_URL", "$MY_DOCKER_REGISTRY_PW") {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
