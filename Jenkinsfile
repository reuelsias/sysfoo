pipeline {
    agent any

    tools{
        maven 'Maven 3.9.9'
    }

    stages {
        stage('build') {
            steps {
                echo 'compiling sysfoo app...'
                sh 'mvn compile'
            }
        }

        stage('test') {
            steps {
                echo 'running unit tests...'
                sh 'mvn clean test'
            }
        }

        stage('package') {
            steps {
                echo 'packaging the app...'
                sh 'mvn package -DskipTests'
            }
        }
    }

    post {
        success {
            echo 'Pipeline concluded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
