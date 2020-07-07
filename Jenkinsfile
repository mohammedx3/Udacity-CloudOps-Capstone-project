pipeline {
     agent any
     stages {
         stage('Lint HTML & Dockerfile') {
              steps {
                  sh 'tidy -q -e *.html'
                  echo 'Linting HTML'
                  sh '/bin/hadolint Dockerfile'
                  echo 'Linting Dockerfile'
              }
         }
         stage('Build image') {
             steps{
	            echo 'Building Docker image...'
                withCredentials([usernamePassword(credentialsId: 'docker-creds', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                     sh '''
						docker build -t mohammedx3/capstone .
					    '''
                }
      }
     }
}
}