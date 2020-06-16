pipeline {
    agent any
    environment {
        DOCKER_IMAGE_NAME = "dchakrab/customer
    stages {
        stage('MVN Built') {
            steps {
                git 'https://github.com/dchakrabarti/microservice-kubernetes.git'
                sh "mvn -Dmaven.test.failure.ignore=true clean package -f /Users/dipankarchakrabarti/microservice-kubernetes/microservice-kubernetes-demo/"
            }
        }
        stage('Dockerizing') {
            steps {
               sh "cp -R /Users/dipankarchakrabarti/microservice-kubernetes/  /Users/dipankarchakrabarti/.jenkins/workspace/"
               sh 'cd /Users/dipankarchakrabarti/.jenkins/workspace/microservice-kubernetes-demo/'
               sh "export PATH=$PATH;/usr/local/bin/docker"
               sh './docker-build.sh'
            }
        }    
        stage('DeployToProduction') {   
            steps {
                input 'Deploy to Production?'
                milestone(1)
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'microservices.yaml',
                )   
            }   
        }   
    }   
}   
