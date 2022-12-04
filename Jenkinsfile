pipeline {
  agent any
stages {
    
    stage('Clone repository') {
      steps {
            checkout scm
           }
      }
    stage('Update GIT') {
      steps {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {

                        sh "git config user.email rsoleimany@yahoo.com"
                        sh "git config user.name  RozWhite"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+rozitadocker123/mlops-jenkins.*+rozitadocker123/mlops-jenkins:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/mlops-kubernetesmanifest.git HEAD:main"
                        
      }
    }
  }
}
}
}
}

