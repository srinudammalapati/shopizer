pipeline {
    agent {label 'SPRING'}
    parameters {
       string (name: 'maven_goal', defaultValue: 'package', description: 'build the code')
        choice (name: 'BRANCH_TO_BUILD', choices: ['master', 'dev', 'qa'], description: 'CHOOSE TO BANCH')
    }
    triggers {pollSCM '* * * * *'}
    stages {
        stage('clone the code'){
            steps{
                git url: 'https://github.com/srinudammalapati/shopizer.git'
                branch: "${params.BRANCH_TO_BUILD}"
            }
        }
        stage('build the code'){
            steps{
                sh "mvn ${params.maven_goal}"
            }
        }
        stage('Archive the artifact'){
            steps{
                archive includes: '**/target/*.jar'
            }
        }
        stage('Archivr Junit results'){
            steps{
                junit testResults: '**/target/surefire-reports/*.xml'
            }
        }
    }
}