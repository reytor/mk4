pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building......'
        sh 'docker build -t app:test .'
      }
    }
    stage('Test') {
      steps {
        echo 'Testing......'
        docker run --rm --name app -itd -p 80:80  app:test
        sh 'nc -vz localhost 80'
        sh 'docker stop app'
      }
    }
    stage('Push Registry') {
      steps {

       echo 'Push withCredentials'
       withCredentials([usernamePassword(credentialsId: '09ce601e-8e59-4bd6-81aa-b74d67adabab',
                       passwordVariable: 'password', usernameVariable: 'user')]) {
          // some block

           sh 'docker tag app:test shoggun/app:stable'
           sh 'docker push shoggun/app:stable'
      }


      }
    }
  }
}