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
                script {
                    myapp = docker.build("${ECR_REGISTRY_URI}/demo:${env.BUILD_ID}")
                }
            }
        }
        stage("Push image to ECR") {
            steps {
                script {
                    docker.withRegistry('https://${ECR_REGISTRY_URI}', 'ecr:eu-west-1:demo-ecr-credentials') {
                        myapp.push("latest")
                        myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
        stage('Deploy to EKS') {
            steps {
                sh "sed -i 's/hello:latest/hello:${env.BUILD_ID}/g' deployment.yaml"
                step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
            }
        }
    }
}