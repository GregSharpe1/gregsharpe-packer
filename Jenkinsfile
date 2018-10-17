pipeline {

  agent any
  environment {
    AWS_ACCESS_KEY = credentials('JenkinsPacker_Public')
    AWS_SECRET_ACCESS_KEY = ('JenkinsPacker_Private')
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