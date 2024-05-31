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
                sh '''
               
                python3 -m venv venv
                source venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }
        stage('Run Tests') {
            steps {
                sh 'source venv/bin/activate && pytest'
            }
        }
        stage('Build') {
            steps {
                sh 'source venv/bin/activate && python setup.py sdist bdist_wheel'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                source venv/bin/activate
                # Add your deployment script here
                echo "Deploying application..."
                '''
            }
        }
    }
   
}
