node {
    def app
    
    env.IMAGE = 'laly9999/node-app-ibt'

    stage('Clone repository') {
             git branch: 'main', url: 'https://github.com/lily4499/node-app-ibt-manifest.git'  
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'lily-git-credentials', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //script {def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')}
                        sh "git config user.email konissil@gmail.com"
                        sh "git config user.name lily4499"
                        //sh "git switch master"
                        sh "cat rollout.yml"
                        sh "sed -i 's+${IMAGE}.*+${IMAGE}:${IMAGETAG}+g' rollout.yml"
                        sh "cat rollout.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job Rolloutmanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/node-app-ibt-manifest.git HEAD:main"
             }
         }
     }
  }
}
