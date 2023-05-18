pipeline{
    
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS=credentials( 'elif-dockerhub')
    }
    stages {
        
        stage('Clone repository') {
            
            steps {
                git branch: 'main', url: 'https://github.com/EAS-Elif/api-frontend.git'
            }
        }
        
        stage('Build image') {
        
            steps {
                sh 'docker build -t eliferdemeas/api-frontend:latest .'
            }
        }
        
        stage('Login') {   
            
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        
        stage('Push') {
         
            steps {
                sh 'docker push eliferdemeas/api-frontend:latest '
            }
        }
        stage('Post') {
    
            steps {
                 sh 'docker logout'
            }
        }
    }
}