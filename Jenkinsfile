@Library("myLibrary") _

pipeline {
    agent any

    environment {
        GITHUB_TOKEN = credentials('mahmoudanwer_github_token')
        GITHUB_USERNAME = "mahmoud-anwer"
        REPO_OWNER = "mahmoud-anwer"
        REPO_NAME = "k8s-application-config"
        TARGET_DIRECTORY = "k8s-config"
        SERVICE_NAME = "api"
        BASE_BRANCH = "main"
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
                    echo "test" > ${TARGET_DIRECTORY}/test.file
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
