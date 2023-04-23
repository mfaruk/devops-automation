pipeline{
    agent any
   
    stages{
        stage('build maven project'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/mfaruk/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage('build docker image'){
            steps{
                script{
                    sh 'sudo docker build -t devops-automation-integration .'
                }
            }
        }
        stage('push docker image to dockerhub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpassword', variable: 'dockerhubpassword')]) {
                     sh 'sudo docker login -u dadasol -p ${dockerhubpassword}'
                    }
                    sh 'sudo docker tag devops-automation-integration dadasol/devops-automation-integration'
                    sh 'sudo docker push dadasol/devops-automation-integration'
                    
                }
            }
        }
    }
}