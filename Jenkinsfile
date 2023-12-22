pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        script {
          checkout scm
        }

      }
    }

    stage('build') {
      steps {
        sh 'cd scripts'
        sh '''
    chmod +x scripts/build.sh'''
        sh 'script scripts/build.sh'
      }
    }

    stage('test') {
      steps {
        sh 'chmod +x scripts/test.sh'
        sh 'script scripts/test.sh'
      }
    }

    stage('docker build') {
      steps {
        script {
          docker.build("${registry}:${env.BUILD_ID}")
        }

      }
    }

    stage('docker push') {
      steps {
        script {
          docker.withRegistry('','dockerhub_id'){
            docker.image("${registry}:${env.BUILD_NUMBER}").push()}
          }

        }
      }

    }
    environment {
      registry = 'meliaszkowalska/mek_docker'
    }
  }