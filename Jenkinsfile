pipeline {
    agent {
        label 'default'
    }

    triggers {
        githubPush() 
    }

    stages {
        stage('Build') {
            steps {
                 container('kubectl') {
                    sh 'kubectl get nodes'
                }
            }
        }
    }
}