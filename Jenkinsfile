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
    post {
        always {
            archiveArtifacts artifacts: '**/results.xml', allowEmptyArchive: true
            junit 'results.xml'
            sh 'deactivate'
        }
        success {
            slackSend(channel: '#your-channel', message: "Build ${env.BUILD_NUMBER} succeeded.")
        }
        failure {
            slackSend(channel: '#your-channel', message: "Build ${env.BUILD_NUMBER} failed.")
        }
    }
}
