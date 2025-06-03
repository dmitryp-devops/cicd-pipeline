pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: "${GIT_BRANCH}", url: 'ssh://git@github.com:dmitryp-devops/cicd-pipeline.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("node${GIT_BRANCH}:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Run') {
            steps {
                sh "docker stop ${GIT_BRANCH}"
                sh "docker run -d --name ${GIT_BRANCH} -p 3001:3000 --rm node${GIT_BRANCH}:${env.BUILD_NUMBER}"
            }
        }
    }
}
