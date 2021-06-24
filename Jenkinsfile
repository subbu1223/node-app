pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t devopsb5/nodeapp:${DOCKER_TAG} "
            }
        }
    }
}


stage('DockerHub Push'){
            steps{
                withCredentials([string(credentialsId: 'devopsb5', variable: 'dockerHubPwd')]) {
                    sh "docker login -u devopsb5 -p ${dockerHubPwd}"
                    sh "docker push devopsb5/nodeapp:${DOCKER_TAG}"
                }
            }
        } 


def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
