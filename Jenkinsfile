pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        stage('List files in workspace') {
            steps {
                sh 'ls -la'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                sh 'scp target/*.war user@server:/var/lib/tomcat/webapps/'
            }
        }
    }
}
