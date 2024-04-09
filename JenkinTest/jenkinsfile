pipeline {
    agent any
    stages {
        stage('Git checkout') {
            steps {
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [],
                          submoduleCfg: [],
                          userRemoteConfigs: [[url: 'https://github.com/virat-2023/DeploymentTest.git']]])
            }
        }
        stage('Build and test') {
            steps {
                sh 'docker stop my-container'
                sh 'docker rm my-container '
                sh 'dotnet build'
                
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t images -f JenkinTest/Dockerfile .'
            }
        }
        
        stage('Deploying'){
            steps{
                sh 'docker run -d -p 8081:80 --name my-container images'

            }
        }
    }
}
