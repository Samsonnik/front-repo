pipeline {
    agent {
        kubernetes {
            label 'my-jenkins-jenkins-agent'
        }
    }

    environment {
        DEPLOY_CHART_NAME = 'front-chart'
        DEPLOY_NS         = 'front'
    }

    triggers {
        githubPush() 
    }

    stages {
        stage('Build') {
            steps {
                 container('helm') {
                    sh 'helm upgrade --install $DEPLOY_CHART_NAME ./helm/front -f ./helm/front/values.yaml -n $DEPLOY_NS'
                }
            }
        }
    }
}