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
               export MINIKUBE_HOME=/var/lib/jenkins
               export PATH=$PATH:/usr/local/bin

               minikube status || minikube start --driver=docker --force

               kubectl get nodes
               kubectl apply -f deployment.yaml
               kubectl apply -f service.yaml
            '''
    }
    }
    }
}
