pipeline {
    agent {
        label 'my-jenkins-jenkins-agent'
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