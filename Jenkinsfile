pipeline {
    agent {
        kubernetes {
            label 'my-jenkins-jenkins-agent'
        }
    }

    environment {
        IMAGE_NAME = 'front-image'
        IMAGE_VER = '1.0.0'
        DOCKER_FILE_PATH = './java-app-main/front/dockerfile'
        DOCKER_FILE_FILES = './java-app-main/front/'
        DEPLOY_CHART_NAME = 'front-chart'
        DEPLOY_NS = 'front'
        CRED_ID = 'eb4b7a94-1a75-4571-87e0-7d2303525122'
    }

    stages {
        stage('Build') {
            steps {
                container('podman') {
                    withCredentials([usernamePassword(
                        credentialsId: env.CRED_ID, 
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS')]) {
                            sh '''
                            echo "$DOCKER_PASS" | podman login docker.io -u "$DOCKER_USER" --password-stdin
                            podman build -f $DOCKER_FILE_PATH -t $IMAGE_NAME:$IMAGE_VER $DOCKER_FILE_FILES
                            podman tag $IMAGE_NAME:$IMAGE_VER $DOCKER_USER/$IMAGE_NAME:$IMAGE_VER
                            podman push $DOCKER_USER/$IMAGE_NAME:$IMAGE_VER
                            '''
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                container('helm') {
                    sh 'helm upgrade --install $DEPLOY_CHART_NAME ./helm/front -f ./helm/front/values.yaml -n $DEPLOY_NS --create-namespace'
                }
            }
        }
    }
}