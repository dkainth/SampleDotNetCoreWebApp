pipeline{
    agent any

    environment{
        dockerImage = ''
    }

    stages{
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
                    withCredentials([usernamePassword( credentialsId: "$MY_DOCKER_REGISTRY_PW", usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        docker.withRegistry("https://$MY_DOCKER_REGISTRY_URL", "$MY_DOCKER_REGISTRY_PW") {
                            sh "docker login -u ${USERNAME} -p ${PASSWORD} https://$MY_DOCKER_REGISTRY_URL"
                            dockerImage.push()
                        }
                    }
                }
            }
        }
    }
}
