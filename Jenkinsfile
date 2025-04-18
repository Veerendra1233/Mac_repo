pipeline {
    agent {
        docker { image 'lachlanevenson/k8s-kubectl:v1.27.3' }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Deploy to Minikube') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
    post {
        failure {
            echo 'Deployment Failed!'
        }
    }
}
