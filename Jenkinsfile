pipeline {
    agent any
    environment {
        PATH = "E:\\minikube\\minikube;$env:PATH"
    }
    stages {
        stage('git') {
            steps {
                git branch: 'main', credentialsId: '64338209-c2d5-4594-a04d-6672d7838d12', url: 'https://github.com/joel2500/kubernetes.git'
            }
        }
        stage('kubernetes deployment') {
            steps {
                bat 'kubectl apply -f nginx-deployment.yaml'
                bat 'kubectl apply -f nginx-service.yaml'
                bat 'minikube service name --url'
            }
        }                             
    }
}
post {
    always {
        emailext body: 'The kunernetes deployment has completed. Status: ${currentBuild.result}', subject: 'Terraform Build Notification', to: 'joelstephen00@gmail.com'
    }
}

