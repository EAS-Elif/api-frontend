pipeline{
    
    agent any
    
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
        
        stage('Push Docker Image') {
         
            steps {
                script{
                   withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASSWORD', usernameVariable: 'USER')]) {
                                           sh '''docker login -u "$USER" -p "$PASSWORD"
                    docker push eliferdemeas/api-frontend:latest'''
                   }
                }
                
            }
        }
        stage('Post') {
    
            steps {
                 sh 'docker logout'
            }
        }
    }
}
