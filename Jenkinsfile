pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building......'
        sh 'docker build -t app:test  .'
      }
    }
    stage('Test') {
      steps {
        echo 'Testing......'
        sh 'docker run --rm --name app -itd -p 80:80  app:test'
        sh '/bin/nc -vz localhost 80'
      }
      post{
        always{
            sh 'docker container stop app'
        }
      }
    }
    stage('Push Registry') {
      steps {
            echo 'Push Registring......'
             sh 'docker tag app:test shoggun/app:stable'
             sh 'docker push shoggun/app:stable'
      }
    }
  }
}