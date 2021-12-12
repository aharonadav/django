pipeline {
  environment {
    imagename = "django"
    ecrurl = "https://553686865554.dkr.ecr.eu-west-1.amazonaws.com/django"
    ecrcredentials = "ecr:eu-west-1:ecr-ismail"
    dockerImage = ''
  } 
  agent any
  stages {
    stage('Checkout external proj') {
        steps {
            git branch: 'main',
                credentialsId: 'github-token',
                url: 'https://github.com/aharonadav/django.git'

            sh "ls -lat"
        }
    }
    stage('Building image') {
      agent { label "django-node"}
        steps{
          script {
              def customImage = docker.build("aharonadav/django:${env.BUILD_ID}")
          }
        }
    }
  }  
}
