pipeline {
    agent {
        kubernetes {
            label 'my-jenkins-jenkins-agent'
        }
    }

    triggers {
        githubPush() 
    }

    stages {
        stage('Build') {
            steps {
                 container('helm') {
                    sh 'helm upgrade --install front ./helm/front -f ./helm/front/values.yaml -n front'
                }
            }
        }
    }
}