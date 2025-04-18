pipeline {
       agent {
        docker {
            image 'lachlanevenson/k8s-kubectl:v1.27.3'
            args '-v $HOME/.kube:/root/.kube'  // Mount kubeconfig for Minikube
        }
    }

    environment {
        KUBECONFIG = '/root/.kube/config'
    }
 
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub
        git url: 'https://github.com/Veerendra1233/Mac_repo.git', branch: 'main'
                
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

