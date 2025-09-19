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
                    sh 'cd helm/front'
                    sh 'helm install back ./ -n default'
                }
            }
        }
    }
}