pipeline {
    agent any
    environment{
      aws-credentials = "07898a7f-5320-4381-b86e-2d8885d6862f"}	
      
      stages {
          stage('Checkout Source'){
              deleteDir()
              checkout scm
          }
          
          stage('angular build'){
              sh "npm install"
              sh "ng build"
          }

          stage('s3 upload'){
              withAWS(region:"ca-central-1",credentials:"${aws-credentials}") {
                  sh "cd dist && aws s3 sync . s3://test-angular-kavya" --delete
              }
          }






      }
}