pipeline {
    agent any
    environment {
        PATH = "${PATH}:/usr/local/bin/bandit"
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/fadhriza/sast-demo-app.git', branch: 'main'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'python3 install bandit --user'
                sh 'python3 install --upgrade pip'
            }
        }
        stage('SAST Analysis') {
            steps {
                sh 'bandit -f xml -o bandit-output.xml -r . || true'
                recordIssues tools: [bandit(pattern: 'bandit-output.xml')]
            }
        }
    }
}
