pipeline {
    agent any
    environment{
      aws_credentials = "$your_credentials"}	

    tools {nodejs "nodejs"} 
      
      stages {
          stage('Checkout Source'){
              steps{
                deleteDir()
                checkout scm
              }
          }
          
          stage('angular build'){
              steps{
                sh "npm install --legacy-peer-deps"
                // sh "npm install --force"
                sh "npm run ng build"
              }
          }

          stage('s3 upload'){
              steps{
              withAWS(region:"ca-central-1",credentials:"${aws_credentials}") {
                  sh "cd dist/angular-calculator/ && aws s3 sync . s3://test-angular-kavya --delete"
              }
              }
          }






      }
}
