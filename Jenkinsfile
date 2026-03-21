pipeline {

    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/rajkumardevaraj92-debug/java-web-app.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Upload Artifact to S3') {
            steps {
                sh 'aws s3 cp target/java-web-app-1.0.jar s3://maven-jenkins-server-bucket/'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh '''
                scp target/java-web-app-1.0.jar ec2-user@65.2.190.151:/home/ec2-user/
                ssh ec2-user@65.2.190.151 "java -jar java-web-app-1.0.jar"
                '''
            }
        }

    }

}
