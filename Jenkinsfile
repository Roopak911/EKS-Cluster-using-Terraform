pipeline {
    agent any
    triggers {
    githubPush()
    }    
    stages {
        stage('Git-checkout') {
            steps {
                sh 'sudo yum install git -y'
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'roopak-git', url: 'https://github.com/Roopak911/EKS-Cluster-using-Terraform.git']])
            }
        }
        stage('run terraform') {
            steps {
                sh '''
		        sudo cd /var/lib/jenkins/workspace/aws-infra/
		        terraform init
                terraform plan
                terraform apply --auto-approve
                '''
            }
        }
        stage('install eksctl') {
            steps {
                sh '''
                bash eksctl.sh
                '''
            }
        }
        stage('install kubectl') {
            steps {
                sh '''
                bash kubectl.sh
                '''
            }
        }
        stage('terraform destroy') {
            steps {
                sh 'terraform destroy --auto-aprove'
            }
        }                     
    }
}
