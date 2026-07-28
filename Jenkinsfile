pipeline {
    agent any

    environment {
        VENV = 'venv'
        DOCKER_IMAGE = 'angy1133/test-flask'
    }

    stages {
        stage('Checkout git') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/angieee11/test-flask.git'
            }
        }

        stage('set up the venv') {
            steps {
                sh '''
                    python3 -m venv $VENV
                    $VENV/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('RUN THE TESTS') {
            steps {
                sh '$VENV/bin/python -m unittest discover -s tests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t angy1133/test-flask:$BUILD_NUMBER .
                    docker tag angy1133/test-flask:$BUILD_NUMBER angy1133/test-flask:latest
                '''
            }
        }
    }
}
