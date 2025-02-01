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
        // Upgrade pip for Python on Windows
        bat 'C:\\Users\\DELL\\AppData\\Local\\Programs\\Python\\Python312\\python -m pip install --upgrade pip'
    }
}

        stage('Install Dependencies') {
            steps {
                // Set up virtual environment and install dependencies
                sh '''
                    python -m venv ${VENV_DIR}
                    ${VENV_DIR}\\Scripts\\activate
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
                    ${VENV_DIR}\\Scripts\\activate
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
