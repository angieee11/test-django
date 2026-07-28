pipeline {
    agent any

    environment {
        VENV = 'venv'
        DOCKER_IMAGE = 'angy1133/test-flask'
    }

    stages {
        stage('Checkout Git') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/angieee11/test-flask.git'
            }
        }

        stage('Set up VENV') {
            steps {
                sh '''
                    python3 -m venv $VENV
                    $VENV/bin/python -m pip install --upgrade pip
                    $VENV/bin/pip install -r requirements.txt
                '''
            }
        }

        stage('Run the Tests') {
            steps {
                sh '$VENV/bin/python -m unittest discover -s tests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t $DOCKER_IMAGE:$BUILD_NUMBER .
                    docker tag $DOCKER_IMAGE:$BUILD_NUMBER $DOCKER_IMAGE:latest
                '''
            }
        }
    }
}
            }
        }
    }
}
