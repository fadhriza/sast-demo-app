pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/fadhriza/sast-demo-app.git', branch: 'main'
            }
        }
        
        stage('Install Dependencies') {
    steps {
        sh '''
            python3 -m venv venv
            source venv/bin/activate
            pip3 install bandit
            pip3 install --upgrade pip
        '''
    }
}

stage('SAST Analysis') {
    steps {
        sh '''
            source venv/bin/activate
            bandit -f xml -o bandit-output.xml -r . || true
        '''
        recordIssues tools: [bandit(pattern: 'bandit-output.xml')]
    }
}

    }
}
