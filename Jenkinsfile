pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building...'
        sh 'docker build -t app:test  .'
      }
    }
    stage('Test') {
      steps {
        echo 'Testing....'
        sh '/bin/nc -vz localhost 22'
      }
    }
    stage('Push Registry') {
      steps {
             sh 'docker tag app:test app:stable'
             sh 'docker push app:test app:stable'
      }
    }
  }
}