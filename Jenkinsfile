pipeline {
       agent any


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
        stage('Set up kubectl') {
            steps {
                script {
                    // Install kubectl (if not already installed) and point to Minikube's kubeconfig
                    sh '''
                    if ! command -v kubectl &> /dev/null
                    then
                        echo "kubectl could not be found, installing..."
                        curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.27.3/bin/linux/amd64/kubectl
                        chmod +x kubectl
                       sudo mv kubectl /usr/local/bin/
                    fi
                    '''
                    // Set kubeconfig to Minikube's local Kube config
                    sh 'export KUBEVERSION=$(minikube version | awk "{print $3}" | tr -d "v")'
                    sh 'eval $(minikube -p minikube docker-env)' // Ensure Minikube's docker daemon is set up for kubectl
                }
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

