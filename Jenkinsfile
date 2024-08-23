pipeline {
    agent any
    environment {
        VENV = 'venv'  // Directory for the Python virtual environment
    }
    stages {
        stage('Clone source code Github repo') {
            steps {
                git branch: 'main', url: 'https://github.com/NandanaAsha/python-project-template.git'
            }
        }
        
        stage('Setup Python Environment') {
            steps {
                // Install virtualenv and create a virtual environment
                sh 'python3 -m venv $VENV'
                sh 'source $VENV/bin/activate'
            }
        }
        
        stage('Install Dependencies') {
            steps {
                // Install project dependencies specified in requirements.txt
                sh '''
                source $VENV/bin/activate
                pip3 install -r requirements.txt
                pip3 install wheel setuptools
                '''
            }
        }
        
        stage('Package Application') {
            steps {
                // Build the package
                sh '''
                source $VENV/bin/activate
                python3 setup.py sdist bdist_wheel
                '''
            }
        }
        
        stage('Run Test on specific file') {
            steps {
                // Run the tests using pytest or another testing framework
                sh '''
                PYTHONPATH=./project_name pytest tests/test_ops.py
                '''
            }
        }

        stage('Run a specific python script') {
            steps {
                sh 'python3 ./project_name/ops.py'
            }
        }
    }
    
    post {
        always {
            // Clean up the workspace and deactivate virtual environment
            sh 'rm -rf $VENV'
            cleanWs()
        }
        failure {
            echo 'Build failed!'
        }
        success {
            echo 'Build succeeded!'
        }
    }
    
}
