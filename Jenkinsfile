pipeline {
    agent {
        label: AGENT1
    }
    environment {
        appversion: ''
        REGION = "us-east-1"
        ACC_ID = "576195058746"
        PROJECT = "roboshop"
        COMPONENT = "catalogue"
    }
    options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds()
    }
    parameters {
        string(name: 'appVersion', description: 'Image version of the application')
        choice(name: 'deploy_to', choices: ['dev', 'qa', 'prod'] description: 'pick the environment')
    }
    //build
    stages {
        stage (deploy) {
            steps {
                script {
                    withAWS (credentials : 'aws_creds', region: 'us-east-1') {
                        sh """
                        aws eks update-kubeconfig --region $REGION --name "$PROJECT-${params.deploy_to}"
                        kubectl get nodes
                        """
                    }
                }
            }
        }
    }

}