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
                sh 'mvn clean package'
            }
        }
        stage('Build') {
          steps {
                sh 'ls -la'
              
            }
        }
        stage('Test') {
        steps {
                sh 'ls -la'
            }
        }
        stage('Deploy to Tomcat') {
          steps {
                sh 'ls -la'
            }
        }
    }
}
