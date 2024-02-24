pipeline {
    agent any
    environment {
        PATH = "$PATH:/opt/apache-maven-3.9.6/bin"
    }
    stages {
        stage('Clone repository') {
            steps {
                git branch: 'main', credentialsId: 'SHABARI-GIT-DETAILS', url: 'https://github.com/medashabari/mavensample.git'
            }
        }
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['ec2-user']) {
                    sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/gitmvntomcatproject/target/Maven-app-02.war ubuntu@18.209.112.146:/home/ubuntu/apache-tomcat-9.0.85/webapps"
                }
            }
        }
    }
}
