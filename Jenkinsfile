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
        stage('Install Terraform') {
            steps {
                sh ''' 
                sudo yum install -y yum-utils
		sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
		sudo yum -y install terraform
		'''
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
    }
}
