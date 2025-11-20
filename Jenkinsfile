pipeline {
    agent {
        label 'AGENT-1'
    }
    environment {
        appVersion = ""
        ACC_ID  = "" 
        PROJECT = "roboshop" 
        REGION  = "us-east-1" 
        COMPONENT = "catalogue"  
    }
    options {
        timeout(time: 30, unit: 'MINUTES') 
        disableConcurrentBuilds() 
        ansiColor('xterm')
    }
    parameters {
        string(name: 'appVersion', description: 'Image version of the application')
        choice(name: 'deploy_to', choices: ['dev', 'qa', 'prod'], description: 'Pick the Environment')
    }
    stages {
        stage ('Deploy') {
            steps {
                script {
                    withAWS(credentials: 'aws-creds', region: 'us-east-1') {
                        sh """
                          aws eks update-kubeconfig --region $REGION --name "$PROJECT-${params.deploy_to}" 
                          kubectl get nodes 
                          kubectl apply -f 01-namespace.yaml
                          sed -i "s/IMAGE_VERSION/$params.appVersion}/g" values-${params.deploy_to}.yaml 
                          helm upgrade --install $COMPONENT -f values-${params.deploy_to}.yaml -n $PROJECT . 
                        """
                    }
                }
            }
        }
    }
    post {
        always {
            echo "I will always say HELLO AGAIN!"
            deleteDir() 
        }
        success {
            echo "Success"
        }
        failure {
            echo "Failure"
        }
    }
}