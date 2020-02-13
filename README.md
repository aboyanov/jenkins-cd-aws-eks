# Simple CI/CD with Jenkins to AWS EKS(K8S) Demo

Jenkins CI/CD to AWS EKS(k8s) Demo:

To test this perform the following steps:

1. change the content of the "index.html" file.
2. push the changes to the repo
3. Go to the Jenkins(deployed on EC2 instance) page: [Jenkins](http://34.243.110.126:8080/job/jenkins-cd-demo/) 
4. Navigate to the job with name "jenkins-cd-demo" and press the "Build Now" button
5. Go to/Refresh the Ngnix page(behind an LB) to see your changes: [Ngninx](http://a23ee206e4e3b11eaa7b7022b75601ce-411609654.eu-west-1.elb.amazonaws.com/)

There isn't configured webhook on push, on purpose, because it will trigger the job too quickly ;)
