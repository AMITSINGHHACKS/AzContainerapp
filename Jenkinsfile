pipeline {
    agent any
    environment {
        client_id  = credentials('azure-client-id')
        client_secret = credentials('azure-client-secret')
        subscription_id = credentials('azure-subscription-id')
        tenant_id = credentials('azure-tenant-id')
    }
    stages {
        stage ('TF Initialising') {
            steps {
                script {
                    sh "terraform init"
                }
            }
        }
        stage ('TF Plan') {
            steps {
                script {
                    sh "terraform plan"
                }
            }
        }
    }
   
}
