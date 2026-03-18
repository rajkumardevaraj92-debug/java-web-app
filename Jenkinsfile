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
                sh 'aws s3 cp target/java-web-app-1.0.jar s3://my-devops-bucket/'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh '''
                scp target/java-web-app-1.0.jar ubuntu@EC2_IP:/home/ubuntu/
                ssh ubuntu@EC2_IP "java -jar java-web-app-1.0.jar"
                '''
            }
        }

    }

}