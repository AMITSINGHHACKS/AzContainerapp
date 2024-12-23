pipeline {
    agent any
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
