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
            dir('demo'){
                script {
                    def customImage = docker.build("aharonadav/django:${env.BUILD_ID}")
                }
            }
        }
    }
    stage('Run image') {
      agent { label "django-node"}
        steps{
          script {
              def output = sh(script:"docker run -d -p 8000:8000 aharonadav/django:${env.BUILD_ID}",
                              returnStatus: true)
              println("${output}")
          }
        }
    }
  }  
}
