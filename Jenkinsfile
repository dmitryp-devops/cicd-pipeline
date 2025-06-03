pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: "${GIT_BRANCH}", url: 'ssh://git@github.com:dmitryp-devops/cicd-pipeline.git', credentialsId: 'github'
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("node${GIT_BRANCH}:v1.0")
                }
            }
        }
        stage('Run') {
            steps {
                sh "docker stop ${GIT_BRANCH}||true"
                sh "docker run -d --name ${GIT_BRANCH} -p 3000:3000 --rm node${GIT_BRANCH}:v1.0"
            }
        }
    }
}
