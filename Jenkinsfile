pipeline {
    agent any 
    stages {
        stage('Git Checkout') {
            steps {
                git 'https://gitlab.com/cloud-devops-assignments/spring-boot-react-example.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Upload or Copy artifact') {
            steps {
                sshagent(['aws-user']) {
                    sh "scp -o StrictHostKeyChecking=no target/*.jar ubuntu@application-server:"
                    sh "ssh -o StrictHostKeyChecking=no ubuntu@application-server  'nohup java -jar react-and-spring-data-rest-0.0.1-SNAPSHOT.jar  > /home/ubuntu/log.txt 2>&1 &'"
                }
            }
        }
    }
}
