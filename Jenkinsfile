pipeline {
    agent any 
    tools {
        maven 'local_maven'
    }

    environment {
        AWS_ACCESS_KEY_ID = credentials('jenkins-aws-secret-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('jenkins-aws-secret-access-key')
        AWS_DEFAULT_REGION = 'us-east-1' // Specify your AWS region here
    }      

    stages {
        stage('Build') {
            steps {
                echo 'build'
            }
        }
        stage('Test') {
            steps {
                echo 'test'
            }
        }
        stage('Publish') {
            steps {
                sh 'mvn clean package -Dmaven.test.skip=true'
            }
            post {
                success {
                    script {
                            sh 'aws configure set region us-east-1 && aws s3 cp ./web/target/*.war s3://myanbucket'
                    }
                }
            }
        }
    }
}
