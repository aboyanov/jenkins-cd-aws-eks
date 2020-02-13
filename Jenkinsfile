pipeline {
    agent any
    environment {
        ECR_REGISTRY_URI = '153657280434.dkr.ecr.eu-west-1.amazonaws.com'
    }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage("Build image") {
            steps {
               sh "docker build -t ${ECR_REGISTRY_URI}/demo:${env.BUILD_ID} ."
            }
        }
        stage("Push image to ECR") {
            steps {
                sh "\$(/usr/local/bin/aws ecr get-login --no-include-email --region eu-west-1)"
                sh "docker push ${ECR_REGISTRY_URI}/demo:${env.BUILD_ID}"
            }
        }
        stage('Deploy to EKS') {
            steps {
                sh "sed -i 's/demo:latest/demo:${env.BUILD_ID}/g' deployment.yaml"
                sh "/usr/bin/kubectl apply -f deployment.yaml"
            }
        }
    }
}