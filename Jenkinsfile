pipeline {
    agent any
    environment {
        IMAGE_NAME = "rehan-devops-app"
        TAR_FILE = "app.tar"
        REMOTE_HOST = "your.vm.ip"
        REMOTE_USER = "ubuntu"
        REMOTE_PASS = "your_password"
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE_NAME ./app'
                sh 'docker save $IMAGE_NAME -o $TAR_FILE'
            }
        }
        stage('Copy to Remote') {
            steps {
                sh 'sshpass -p "$REMOTE_PASS" scp -o StrictHostKeyChecking=no $TAR_FILE $REMOTE_USER@$REMOTE_HOST:/tmp/'
            }
        }
        stage('Ansible Deploy') {
            steps {
                sh 'ansible-playbook -i ansible/inventory ansible/deploy.yaml'
            }
        }
    }
}