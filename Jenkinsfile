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
                    github credentialsId: 'github',
                    url: 'https://github.com/mukeshr-29/gitops-argocd-project-4.git',
                    branch: 'main'
                }
            }
        }
        stage('build docker img') {
            steps {
                script {
                    docker_image = docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }
        stage('push docker img') {
            steps {
                script {
                    docker.withRegistry('', REGISTRY_CREDS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }
                }
            }
        }
    }
}