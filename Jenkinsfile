pipeline{
    agent any

    environment{
        VENV_DIR = 'venv'
    }

    stages{
        stage("cloning from github"){
            steps{
                script{
                    echo 'cloning from github'
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github-token', url: 'https://github.com/johan1704/mlops_project2']])
                }
            }
        }
        stage("making a virtual environment..."){
            steps{
                script{
                    echo 'making a virtual environment'
                    sh ''' 
                    python -m venv ${VENV_DIR}
                    . ${VENV_DIR}/bin/activate
                    pip install --upgrade pip
                    pip install -e .
                    pip install dvc
                    '''
                }
            }
        }

        stage('DVC PUll'){
            steps{
                withCredentials([file(credentialsId:'gcp-key' , variable: 'GOOGLE_APPLICATION_CREDENTIALS')]){
                    script{
                        echo 'DVC Pull...'
                        sh ''' 
                        . ${VENV_DIR}/bin/activate
                        dvc pull
                        '''
                    }
                }
            }
        }

    }
}