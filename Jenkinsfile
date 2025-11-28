pipeline {
    agent any

    environment {
        KUBECONFIG = credentials('k3s-Kubeconfig')
    }

    stages {

        stage('Checkout Kubernetes Manifests') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Omkar8284/Jenkins-Kubernetes-CD.git'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                    kubectl apply -f manifests/deployment.yaml
                    kubectl apply -f manifests/service.yaml
                    kubectl apply -f manifests/ingress.yaml
                '''
            }
        }

        stage('Verify Rollout') {
            steps {
                sh '''
                    kubectl rollout status deployment/demo-app --timeout=60s
                '''
            }
        }
    }
}
