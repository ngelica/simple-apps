pipeline {
    agent { label 'dev-virya' }

    stages {
        stage('Pull SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/ngelica/simple-apps.git'
            }
        }
        
        stage('Build') {
            steps {
                sh'''
                cd app
                npm install
                '''
            }
        }
        
        stage('Testing') {
            steps {
                sh'''
                cd app
                npm test
                npm run test:coverage
                '''
            }
        }
        
        stage('Code Review') {
            steps {
                sh'''
                cd app
                sonar-scanner \ 
                    -Dsonar.projectKey=simple-virya \ 
                    -Dsonar.sources=. \ 
                    -Dsonar.host.url=http://172.23.8.125:9000 \ 
                    -Dsonar.login=sqp_58d8bb42f47e2b44d9b40753c81337f8bc32d577 
                '''
            }
        }
        
        stage('Deploy') {
            steps {
                sh'''
                docker compose up --build -d
                '''
            }
        }
        
        stage('Backup') {
            steps {
                 sh 'docker compose push' 
            }
        }
    }
}