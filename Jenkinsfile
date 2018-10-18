pipeline {

  agent any
  environment {
    AWS_ACCESS_KEY_ID = credentials('JenkinsPacker_Public')
    AWS_SECRET_ACCESS_KEY = credentials('JenkinsPacker_Private')
    PACKER_AMI = sh(script: "aws ec2 describe-images --owner self --query 'Images[*].{ID:ImageId}' | grep -o '\".*\"' | sed 's/\"//g' | cut -d":" -f2")
  }
  parameters {
    string(
      name: 'AWS_REGION',
      defaultValue: 'eu-west-2',
      description: 'Where do you wish to build an image?'
    )
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
          sh "packer validate ${params.AWS_REGION}-ubuntu1604.json"
          slackSend "Your ${params.AWS_REGION} packer image validated!"
	      }
      }
    }
    stage('Build') {
      steps {
        dir('packer-images/') {
          slackSend "Starting packer build in ${params.AWS_REGION}"
          sh "packer build -debug ${params.AWS_REGION}-ubuntu1604.json"
        }
      }
    }
    stage('Cleanup') {
      steps {
        cleanWs()
      }
    }
    stage('Slack Notify') {
      steps {
        slackSend "Completed the packer build in ${params.AWS_REGION}, New AMI ${env.PACKER_AMI}"
      }
    } 
  }
}