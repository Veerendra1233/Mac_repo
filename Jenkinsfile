pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub
git 'https://github.com/Veerendra1233/Mac_repo.git'               
            }
        }
        
        stage('Deploy to Minikube') {
            steps {
                // Apply the deployment.yaml file to Minikube
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
    
    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}

