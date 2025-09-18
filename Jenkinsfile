pipeline {
    agent any

    triggers {
        githubPush() 
    }

    stages {
        stage('Build') {
            steps {
                echo 'Сборка запущена по вебхуку!'
                sh 'echo "Текущая ветка: $BRANCH_NAME"'
            }
        }
    }
}