pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'ssh://git@github.com:dmitryp-devops/cicd-pipeline.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("nodemain:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Run') {
            steps {
                sh "docker stop ${GIT_BRANCH}"
                sh "docker run -d --name ${GIT_BRANCH} -p 3000:3000 --rm nodemain:${env.BUILD_NUMBER}"
            }
        }
    }
}
