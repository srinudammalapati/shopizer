pipeline {
    agent {label 'DOCKER'}
    trigger {
        pollSCM('* * * * *')
    }
    parameters {
       choice(name: 'maven_goal', choices: ['package', 'clean', 'install'], description: 'build the code')
        choice(name: 'branch _to_build', choices: ['main', 'dev', 'qa'], description: 'branch to build')
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
                Archive includes: '**/target/*.jar'
            }
        }
        stage('Archivr Junit results'){
            steps{
                Junit testResult: '**/target/surefire-reports/*.xml'
            }
        }
    }
}