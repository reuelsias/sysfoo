pipeline {
  agent any
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
        sh '''GIT_SHORT_COMMIT=$(echo $GIT_COMMIT | cut -c 1-7)

mvn versions:set -DnewVersion="$GIT_SHORT_COMMIT"
mvn versions:commit'''
        sh 'mvn package -DskipTests'
        archiveArtifacts '**/target/*.jar'
      }
    }

  }
  tools {
    maven 'Maven 3.9.9'
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