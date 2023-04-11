pipeline {
    agent {label 'TERRAFORM'}
    stages {
        stage('clone the code'){
            steps{
                git url: 'https://github.com/srinudammalapati/shopizer.git',
                branch: 'uat'
            }
        }
        stage ('terraform') {
            steps {
                sh 'terraform init'
                sh 'terraform apply -var-file="dev.tfvars" -auto-approve'
           }
        }
    }
}