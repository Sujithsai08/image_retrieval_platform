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
               
                sh 'pip install -r requirements.txt'
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
                echo "Deploying application..."
                '''
            }
        }
    }
    
}
