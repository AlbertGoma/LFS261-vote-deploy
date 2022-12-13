node {
  def app

  stage('Clone repository') {
    

      checkout scm
  }

  stage('Update GIT') {
    script {
      catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
        withCredentials([usernamePassword(credentialsId: 'myAccessToken', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
          //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
          sh "git config user.email 58812649+AlbertGoma@users.noreply.github.com"
          sh "git config user.name AlbertGoma"
          sh "git config pull.rebase false"
          sh "git switch main"
          sh "cat vote-ui-deployment.yaml"
          sh "sed -i 's+albertgoma/vote.*+albertgoma/vote:${DOCKERTAG}+g' vote-ui-deployment.yaml"
          sh "cat vote-ui-deployment.yaml"
          sh "git add ."
          sh "git commit -m 'Done by Jenkins Job deployment: ${env.BUILD_NUMBER}'"
          sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/LFS261-vote-deploy.git HEAD:main"
        }
      }
    }
  }
  
  
}
