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
                 container('jnlp') {
                    sh 'kubectl get nodes'
                }
            }
        }
    }
}