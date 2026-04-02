pipeline {
    agent any

    stages {

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'minikube image build -t java-app:v1 .'
            }
        }

        stage('Deploy to Kubernetes') {
    steps {
        sh '''
        export KUBECONFIG=/var/lib/jenkins/.kube/config
        kubectl get nodes
        kubectl apply -f deployment.yaml
        kubectl apply -f service.yaml
        '''
    }
}
    }
}
