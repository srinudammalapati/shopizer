pipeline {
    agent {label 'SPRING'}
    triggers {pollSCM '* * * * *'}
    parameters {
       choice (name: 'maven_goal', choices: ['package', 'clean', 'install'], description: 'build the code')
        choice (name: 'branch_to _build', choices: ['master', 'dev', 'qa'], description: 'build to build')
    }
    stages {
        stage('clone the code'){
            steps{
                git url: 'https://github.com/srinudammalapati/shopizer.git'
                branch: "${params.branch_to_build}"
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