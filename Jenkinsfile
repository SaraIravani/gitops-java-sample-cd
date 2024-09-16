pipeline {
    agent { label "" }
    environment {
              APP_NAME = "java-sample-pipeline"
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

      
    }
}
