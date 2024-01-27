@Library("myLibrary") _

pipeline {
    agent any

    environment {
        newTag = "${env.GIT_COMMIT}"
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                sh """
                    echo "Clone Repository"
                """
            }
        }
        stage('Editing files') {
            steps {
                script{
                    sh """
                    echo "---- ${newTag}"
                    """
                }
            }
        }
        stage('Creating pull request') {
            steps {
                 sh """
                    echo "Creating pull request"
                """
            }
        }
    }
}
