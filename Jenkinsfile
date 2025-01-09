pipeline{
    agent any
    tools{
        maven 'maven_3_5_0'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Sachintha1994/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage('Build Docker image'){
            steps{
                script{
                    sh 'docker build -t sachintha94/devopsintegration .'
                }

            }
        }
        stage('Push image to hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerpwd')]) {
                        sh 'docker login -u sachintha94 -p ${dockerpwd}'
                    }
                    sh 'docker push sachintha94/devopsintegration:latest'
                }
            }
        }
    }
}