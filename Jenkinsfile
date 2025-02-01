pipeline {
    agent any

    environment {
        // Define the Python virtual environment path
        VENV_DIR = "${env.WORKSPACE}/venv"
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository from GitHub
                git branch: 'main', url: 'https://github.com/rishabh25-I3/PYTEST.git'
            }
        }

        stage('Set Up Python Environment') {
            steps {
                // Install virtualenv and create a virtual environment
                sh '''
                    python -m pip install --upgrade pip
                    pip install virtualenv
                    virtualenv venv
                    source venv/bin/activate
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                // Activate the virtual environment and install dependencies
                sh '''
                    source venv/bin/activate
                    if [ -f requirements.txt ]; then
                        pip install -r requirements.txt
                    fi
                '''
            }
        }

        stage('Run Pytest') {
            steps {
                // Run pytest within the virtual environment
                sh '''
                    source venv/bin/activate
                    pytest --maxfail=5 --disable-warnings -q
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and tests completed successfully!'
        }
        failure {
            echo 'Build or tests failed. Check the logs for details.'
        }
    }
}
