pipeline {
    agent any
    
    stages {
       
        
        stage('Build') {
            steps {
                // Install dependencies and build the Python application
                sh 'pip install -r requirements.txt'
                sh 'python setup.py build'
            }
        }
        
        stage('Run Python Script') {
            steps {
                sh 'python image_retrieval.py'
            }
        }
    
        
        stage('Test') {
            steps {
                // Run tests
                sh 'python -m unittest discover tests'
            }
        }
        
        
    }
    
    post {
        success {
            // Send notification on success
            echo 'Python application built, tested, and deployed successfully!'
        }
        failure {
            // Send notification on failure
            echo 'Pipeline failed: Python application build, test, or deploy failed!'
        }
    }
}
