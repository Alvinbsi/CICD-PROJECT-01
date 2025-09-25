pipeline {
    agent any

    stages {
        stage('Pull Code From GitHub') {
            steps {
                git branch: 'main', url: 'https://github.com/Alvinbsi/Devops_Project_SEP12.git'
            }
        }
    stage('Build the Docker image') {
            steps {
                sh 'docker build -t cicdproject /var/lib/jenkins/workspace/cicd-project01'
                sh 'docker tag cicdproject alvinselva/cicdproject:latest'
                sh 'docker tag cicdproject alvinselva/cicdproject:${BUILD_NUMBER}'
            }
        }
    stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push alvinselva/cicdproject:latest'
                sh 'sudo docker image push alvinselva/cicdproject:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/weekendproj/pod.yaml'
                sh 'sudo kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
