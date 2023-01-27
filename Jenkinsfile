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

        stage ('Push Docker Image') {
            steps
                script {
                    docker.withRegistry('https://registry.hub.docker.com','dockerhub')
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                }
        }

        stage ('Deploy Kubernetes') {

            steps {
                withKubeconfig ([credentialsId: 'Kubeconfig']) {
                    sh 'kubectl apply -f ./k8s/deployment.yaml'
                }
            }
        }
    }
    
}
