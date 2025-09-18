pipeline {
    agent {
        label 'jnlp'
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