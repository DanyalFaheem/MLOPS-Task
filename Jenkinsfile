pipeline {
  agent any  
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
  }
    stages {
    stage('Build') {
        steps {
        sh 'docker build -t sentimentanalysis:latest .'
        }
    }
    stage('Login') {
        steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        }
    }
    stage('Push') {
        steps {
        sh 'docker tag sentimentanalysis:latest danyalfaheem/sentimentanalysis:latest'
        sh 'docker push danyalfaheem/sentimentanalysis:latest'
        }
    }
    stage('Execute') {
        steps {
            sh 'docker run -d -p 5000:5000/tcp -p 5000:5000/udp sentimentanalysis:latest'
        }
    }
  }
}
