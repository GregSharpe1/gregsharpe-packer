pipeline {

  agent any
  environment {
    AWS_ACCESS_KEY_ID = credentials('JenkinsPacker_Public')
    AWS_SECRET_ACCESS_KEY = ('JenkinsPacker_Private')
    TEST = 'greg'
  }
  stages {
    stage('Checkout SCM') {
      steps {
        checkout scm
      }
    }
    stage('Validate') {
      steps {
        dir('packer-images/') {
          sh 'packer validate ubuntu1604.json'
	      }
      }
    }
    stage('Build') {
      steps {
        dir('packer-images/') {
          sh 'echo $TEST'
          sh 'echo $AWS_SECRET_ACCESS_KEY'
          sh 'echo $AWS_ACCESS_KEY_ID'
          // sh 'packer build ubuntu1604.json'
        }
      }
    }
  }
}