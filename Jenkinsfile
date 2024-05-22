@Library("myLibrary") _

pipeline {
    agent any

    environment {
        CREDENTIALS_ID = "mahmoudanwer_github_token"
        GITHUB_USERNAME = "mahmoud-anwer"
        REPO_OWNER = "mahmoud-anwer"
        REPO_NAME = "k8s-application-config"
        TARGET_DIRECTORY = "k8s-config"
        SERVICE_NAME = "api"
        BASE_BRANCH = "main"
        COMMIT_HASH = "${env.GIT_COMMIT}"
        DOCKERHUB_CREDENTIALS_ID = "mahmoudanwer_dockerhub_token"
        DOCKERHUB_USERNAME = "anwer95"
    }
    stages {
        stage('DockerHub login') {
            steps {
                script {
                    echo "Logging Dockerhub..."
                    def dockerhub_params = [
                        dockerhub_credentials_id: env.DOCKERHUB_CREDENTIALS_ID,
                        dockerhub_username: env.DOCKERHUB_USERNAME
                    ]
                    loginCR.dockerhub(dockerhub_params)
                }
            }
        }
        stage('Cloning Repository') {
            steps {
                script {
                    echo "Cloning..."
                    def cloneRepo_params = [
                        github_username: env.GITHUB_USERNAME,
                        credentials_id: env.CREDENTIALS_ID,
                        repo_owner: env.REPO_OWNER,
                        repo_name: env.REPO_NAME,
                        target_dir: env.TARGET_DIRECTORY
                    ]
                    cloneRepo(cloneRepo_params)
                }
            }
        }
        stage('Editing files') {
            steps {
                script{
                     echo "Editing..."
                    // sh '''
                    //     echo "---- ${COMMIT_HASH}"
                    // '''
                    sh "touch ./${TARGET_DIRECTORY}/file"
                }
            }
        }
        stage('Creating pull request') {
            steps {
                script {
                    echo "Pull request"
                    def createPR_params = [
                        github_username: env.GITHUB_USERNAME,
                        credentials_id: env.CREDENTIALS_ID,
                        repo_owner: env.REPO_OWNER,
                        repo_name: env.REPO_NAME,
                        target_dir: env.TARGET_DIRECTORY,
                        base_branch: env.BASE_BRANCH,
                        new_branch_name: "test/update-${SERVICE_NAME}-${env.BUILD_ID}",
                        commit_msg: "Update-with-tag-${COMMIT_HASH}"
                    ]
                    createPR(createPR_params)
                }
            }
        }
    }
}
