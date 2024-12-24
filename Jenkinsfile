pipeline {
    agent any
    environment {
        TFVARS_PASSPHRASE = credentials('gpg-passphrase')
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
        stage ('decrypting the tfvars file') {
            steps {
                script {
                    sh "gpg --batch --yes --passphrase $TFVARS_PASSPHRASE -d terraform.tfvars.gpg > terraform.tfvars"
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
        stage ('Removing the tfvars file') {
            steps {
                script {
                    sh "rm -rf terraform.tfvars"
                }
            }
        }
    }
   
}
