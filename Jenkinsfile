pipeline {
    agent any
    tools{
        maven 'maven_3_5_0'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/junaidshaikh77/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'echo "qwerty" | su - minikubeuser'
                    sh 'echo "qwerty" | sudo -S docker build -t devops-integration .'
                }
            }
        }
        stage('Push docker image to dockerHub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u junaidshaikhcr7 -p ${dockerhubpwd}'
}
                    sh 'docker tag devops-integration junaidshaikhcr7/devops-integration:latest'
                    sh 'docker push junaidshaikhcr7/devops-integration:latest'
                }
            }
        }
    }
}
