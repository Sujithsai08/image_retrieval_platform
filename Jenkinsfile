pipeline {
    agent any

  

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Sujithsai08/image_retrieval_platform.git'
            }
        }
        stage('Setup Python Environment') {
            steps {
                sh '''
                if ! command -v python3 &>/dev/null; then
                    sudo apt-get update
                    sudo apt-get install -y python3 python3-venv python3-pip
                fi
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
