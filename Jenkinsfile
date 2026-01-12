pipeline{
    agent any

    stages{
        stage("cloning from github"){
            steps{
                script{
                    echo 'cloning from github'
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-token', url: 'https://github.com/johan1704/mlops_project2']])
                }
            }
        }
    }
}