pipeline {
    agent {label 'TERRAFORM'}
    parameters {
       string (name: 'maven_goal', defaultValue: 'package', description: 'build the code')
        choice (name: 'BRANCH_TO_BUILD', choices: ['master', 'dev', 'qa','uat'], description: 'CHOOSE TO BANCH')
    }
    stages {
        stage('clone the code'){
            steps{
                git url: 'https://github.com/srinudammalapati/shopizer.git',
                branch: "${params.BRANCH_TO_BUILD}"
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