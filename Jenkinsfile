pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World Temo"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
              }
         }
         stage('Security Scan') {
              steps { 
                 aquaMicroscanner imageName: 'alpine:latest', notCompliesCmd: 'exit 1', onDisallowed: 'fail'
              }
         }         
         stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-east-2',credentials:'aws-credentials') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'tammam-jenkins-pipeline')
                  }
              }
         }
     }
}
