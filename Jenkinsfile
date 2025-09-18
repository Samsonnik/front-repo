pipeline {
    agent kubernetes

    triggers {
        githubPush() 
    }

    stages {
        stage('Build') {
            steps {
                kubectl get nodes
            }
        }
    }
}