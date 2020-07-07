pipeline {
    environment {
    registry = "mohammedx3/capstone-project"
    registryCredential = 'docker-creds'
    dockerImage = ''
}
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
        stage('Building image') {
            steps {
                script {
                dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
            }
        stage('Deploy Image') {
            steps{    script {
                docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                }
                }
            }
}
}
}