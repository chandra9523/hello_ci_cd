pipeline {

    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/chandra9523/hello_ci_cd.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                . venv/bin/activate
                python app.py
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                . venv/bin/activate
                pytest
                '''
            }
        }
        

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t chandra9523/hello-ci-cd:latest .'
            }
        }
        stage('Docker Login') {
            steps {
                 withCredentials([usernamePassword(credentialsId: 'dockerhub',
                 usernameVariable: 'cbdocker2525',
                 passwordVariable: 'dckr_pat_EogwUsZ9OvMqxVB8w02ftJTLa0s')]) {

            sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
        }
    }
}

        stage('Push Docker Image') {
            steps {
                sh 'docker push cbdocker2525/hello-ci-cd:latest'
            }
        }

    
    }
}