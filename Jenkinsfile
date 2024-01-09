pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
    stages{
        stage('Build'){
            steps {

                sh 'mvn clean package -Dmaven.test.skip=true'
		    }
            }    
	stage('SonarQube analysis') {
            steps{
		    withSonarQubeEnv(credentialsId: 'sonar-id', installationName: 'sonar') { // You can override the credential to be used
		    sh "mvn clean verify sonar:sonar -Dsonar.projectKey=test -Dsonar.projectName='test'"
    }
		    }
}
}
}
