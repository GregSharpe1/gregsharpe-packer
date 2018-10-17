pipeline {

  agent any
  environment {
    AWS_ACCESS_KEY = 'test access key'
    AWS_SECRET_ACCESS_KEY = 'test secret key'
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
  }
}
