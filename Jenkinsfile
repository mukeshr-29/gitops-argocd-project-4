pipeline {
    agent any
    environment {
        DOCKERHUB_USERNAME = "mukeshr29"
        APP_NAME = "argocd-project"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTRY_CREDS = 'dockerhub'
    }
    stages {
        stage('clean workspace') {
            steps {
                script {
                    cleanWs()
                }
            }
        }
        stage('checkout scm') {
            steps {
                script {
                    git credentialsId: 'github',
                           url: 'https://github.com/mukeshr-29/gitops-argocd-project-4.git',
                           branch: 'main'
                }
            }
        }
    }
}