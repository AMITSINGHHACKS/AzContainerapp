pipeline {
    agent any
    parameters {
        choice(name: "plandestroy", choices: plan,destroy)
    }
    environment {
        TFVARS_PASSPHRASE = credentials('gpg-passphrase')
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
                    sh "terraform ${params.plan-destroy}"
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
        stage ('Clean WS') {
            steps {
                script {
                    cleanWs()
                }
            }
        }
    }
   
}
