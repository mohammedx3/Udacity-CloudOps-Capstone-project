pipeline {
     agent any
     stages {
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
                  sh '''docker run --rm -i hadolint/hadolint < Dockerfile'''
              }
         }
     }
}