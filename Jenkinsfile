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
        DEPLOY_CHART_NAME = 'front-chart'
        DEPLOY_NS         = 'front'
    }

    stages {
        stage('Build') {
            steps {
                container('podman') {
                    sh 'podman build -f $DOCKER_FILE_PATH -t $IMAGE_NAME:$IMAGE_VER'
                }
            }
        }
    }

    stages {
        stage('Deploy') {
            steps {
                 container('helm') {
                    sh 'helm upgrade --install $DEPLOY_CHART_NAME ./helm/front -f ./helm/front/values.yaml -n $DEPLOY_NS'
                }
            }
        }
    }
}