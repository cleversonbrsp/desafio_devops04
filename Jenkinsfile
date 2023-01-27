pipeline {
    agent any

    steges {

        stage ('Build Docker Image') {
            steps {
                script {
                    dockerapp = docker.build("thefly72003/kube-news:${env.BUILD_ID}", '-f ./src/Dockerfile ./src')
                }
            }
        }
    }
}