node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([gitUsernamePassword(credentialsId: 'githubcred', gitToolName: 'Default')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email kranthikirang@gmail.com"
                        sh "git config user.name kranthikg"
                        //sh "git switch master"
                        sh "cat Deployment.yaml"
                        withEnv(["DOCKER_IMAGE_TAG=kranthikg/sharedlibimage:${BUILD_ID}"]) {
                          sh "sed -i 's+kranthikg/sharedlibimage.*+${DOCKER_IMAGE_TAG}+g' Deployment.yml"  }
                        # sh "sed -i 's+kranthikg/sharedlibimage.*+${DOCKER_IMAGE_TAG}+g' Deployment.yml"
                        sh "cat Deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://github.com/KranthiKG/Devops-Integration-SharedLib.git HEAD:main"
      }
    }
    
  }
}
}