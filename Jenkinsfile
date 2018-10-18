pipeline {

  agent any
  environment {
    AWS_ACCESS_KEY_ID = credentials('JenkinsPacker_Public')
    AWS_SECRET_ACCESS_KEY = credentials('JenkinsPacker_Private')
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
          sh 'packer validate london-ubuntu1604.json'
	      }
      }
    }
    stage('Build') {
      steps {
        dir('packer-images/') {
          sh 'packer build -debug london-ubuntu1604.json'
        }
      }
    }
  }
}