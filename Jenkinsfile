pipeline {
    agent any
    stages {
        stage('Install kubectl') {
            steps {
                script {
                    // Check if kubectl is installed
                    sh '''
                    if ! command -v kubectl &> /dev/null
                    then
                        echo "kubectl could not be found, installing..."
                        curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.27.3/bin/darwin/amd64/kubectl
                        chmod +x kubectl
                        mkdir -p /home/jenkins/bin
                        mv kubectl /home/jenkins/bin/
                        export PATH=$PATH:/home/jenkins/bin
                    fi
                    '''
                }
            }
        }
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
