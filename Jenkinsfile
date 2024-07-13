pipeline {
    agent any

    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Karthik-Devopss/Project.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t projectimage /var/lib/jenkins/workspace/trialproject'
                sh 'sudo docker tag projectimage sbkarthi05/projectimage:latest'
                sh 'sudo docker tag projectimage sbkarthi05/projectimage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push sbkarthi05/projectimage:latest'
                sh 'sudo docker image push sbkarthi05/projectimage:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/trialproject/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
