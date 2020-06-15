pipeline {
    agent any
    
    stages {
        stage('DeployToProduction') {   
            steps {
                input 'Deploy to Production?'
                milestone(1)
                kubernetesDeploy(
                    kubeconfigId: 'kubeconfig',
                    configs: 'microservices.yml',
                )   
            }   
        }   
    }   
}   
