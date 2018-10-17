pipeline {

  agent any
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
