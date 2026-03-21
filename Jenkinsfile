pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/rajkumardevaraj92-debug/java-web-app.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh '''
                scp -o StrictHostKeyChecking=no target/java-web-app-1.0.jar ec2-user@13.232.158.238:/home/ec2-user/
                ssh -o StrictHostKeyChecking=no ec2-user@13.232.158.238 "java -jar /home/ec2-user/java-web-app-1.0.jar &"
                '''
            }
        }

    }
}
