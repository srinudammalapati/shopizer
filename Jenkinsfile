pipeline {
    agent {label 'TERRAFORM'}
    parameters {
       string (name: 'maven_goal', defaultValue: 'package', description: 'build the code')
        choice (name: 'BRANCH_TO_BUILD', choices: ['master', 'dev', 'qa'], description: 'CHOOSE TO BANCH')
    }
    stages {
        stage('clone the code'){
            steps{
                git url: 'https://github.com/srinudammalapati/shopizer.git',
                branch: "${params.BRANCH_TO_BUILD}"
            }
        }
        stage ('Artifactory configuration') {
            steps {
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: "jfrog",
                    releaseRepo: 'dev-libs-release-local',
                    snapshotRepo: 'dev-libs-snapshot-local'
                )
           }
        }
        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'MAVEN_DEFAULT', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'package',
                    deployerId: "MAVEN_DEPLOYER"
                )
            }
        }
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "jfrog"
                )
            }
        }
    }
}