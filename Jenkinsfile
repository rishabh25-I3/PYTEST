pipeline {
    agent any

    environment {
        PYTHON_HOME = 'C:/Users/DELL/AppData/Local/Programs/Python/Python312'
        PATH = "${env.PYTHON_HOME};${env.PYTHON_HOME}/Scripts;${env.PATH}"
        VENV_DIR = "${WORKSPACE}/venv"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/rishabh25-I3/PYTEST.git'
            }
        }

        stage('Set Up Python Environment') {
            steps {
                bat 'C:\\Users\\DELL\\AppData\\Local\\Programs\\Python\\Python312\\python -m pip install --upgrade pip'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat '''
                    C:\\Users\\DELL\\AppData\\Local\\Programs\\Python\\Python312\\python -m venv ${VENV_DIR}
                    ${VENV_DIR}\\Scripts\\activate
                    if exist requirements.txt (
                        ${VENV_DIR}\\Scripts\\pip install -r requirements.txt
                    )
                '''
            }
        }

        stage('Run Pytest') {
            steps {
                bat '''
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
