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
             stage('K8S Deploy')  {
            steps {
                withAWS(credentials: 'aws-creds', region: eksRegion) {
                    sh 'aws eks --region=${eksRegion} update-kubeconfig --name ${eksClusterName}'
                    sh 'kubectl apply -f k8s/uc-capstone-deployment.yml'
                }
            }
        }    

}
}