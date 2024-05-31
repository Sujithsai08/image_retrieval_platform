pipeline {
    agent any

    environment {
        VIRTUAL_ENV = "${WORKSPACE}/venv"
        PYTHON = "${VIRTUAL_ENV}/bin/python"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Sujithsai08/image_retrieval_platform.git'
            }
        }
        stage('Setup Python Environment') {
            steps {
                script {
                    // Check if Python 3 is installed
                    if (!sh(script: 'command -v python3', returnStatus: true)) {
                        // Install Python 3 and required packages
                        sh '''
                            sudo apt-get update
                            sudo apt-get install -y python3 python3-venv python3-pip
                        '''
                    }
                    // Create virtual environment
                    sh 'python3 -m venv venv'
                    // Activate virtual environment
                    sh "${VIRTUAL_ENV}/bin/activate"
                    // Upgrade pip and install requirements
                    sh '''
                        ${PYTHON} -m pip install --upgrade pip
                        ${PYTHON} -m pip install -r requirements.txt
                    '''
                }
            }
        }
        stage('Run Tests') {
            steps {
                sh "${VIRTUAL_ENV}/bin/activate && pytest"
            }
        }
        stage('Build') {
            steps {
                sh "${VIRTUAL_ENV}/bin/activate && python setup.py sdist bdist_wheel"
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                    ${VIRTUAL_ENV}/bin/activate
                    # Add your deployment script here
                    echo "Deploying application..."
                '''
            }
        }
    }
}
