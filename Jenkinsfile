pipeline {
    agent any

    environment {
        VIRTUAL_ENV = "${WORKSPACE}/venv"
        PYTHON = "${VIRTUAL_ENV}/bin/python"
    }

    stages {
        stage('Setup Python Environment') {
            steps {
                script {
                    // Check if Python 3 is installed
                    if (!sh(script: 'command -v python3', returnStatus: true)) {
                        // Update package index without interactive prompt
                        sh 'sudo apt-get update -y'
                        // Install Python 3 and required packages
                        sh '''
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
                script {
                    // Ensure the virtual environment is activated before running tests
                    sh "${VIRTUAL_ENV}/bin/activate && pytest"
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Ensure the virtual environment is activated before building
                    sh "${VIRTUAL_ENV}/bin/activate && python setup.py sdist bdist_wheel"
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Ensure the virtual environment is activated before deployment
                    sh '''
                        ${VIRTUAL_ENV}/bin/activate
                        # Add your deployment script here
                        echo "Deploying application..."
                    '''
                }
            }
        }
    }
}
