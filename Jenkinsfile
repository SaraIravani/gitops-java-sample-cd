pipeline {
    agent any
    environment {
              APP_NAME = "java-sample"
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
               steps {
                   git branch: 'main', credentialsId: 'github', url: 'https://github.com/SaraIravani/gitops-java-sample-cd.git'
               }
        }
       stage("Update the Deployment Tags") {
           steps{
               sh """
                  cat deployment.yaml
                  sed -i 's/\\(APP_NAME\\).*/\\1:${IMAGE_TAG}/g' deployment.yaml || exit 1
                  cat deployment.yaml
               """
           }
       }
       stage("Push the changed deployment file to Git"){
           steps{
               sh """
                  git config --global user.name "sarairavani"
                  git config --global user.email "sarairavani@github.com"
                  git add deployment.yaml
                  git commit -m "Update deployment file"
               """
               withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolsName: 'Default')]){
                   sh "git push https://github.com/SaraIravani/gitops-java-sample-cd main"
               }
           }
       } 
      
    }
}
