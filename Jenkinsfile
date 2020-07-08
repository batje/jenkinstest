pipeline {
  agent {
    label 'cognos'
  }
  tools {
    nodejs "Cognos Node"
  }
  stages {
    stage('Prepare') {
      steps {
        script {
          if (env.BRANCH_NAME == "master") {
            echo "We are in production, lets not do anything yet"
            secretFileName = "MY_SECRET_FILE"
            currentBuild.displayName =  currentBuild.displayName + " PROD"
          } else if (env.BRANCH_NAME == "int") {
            echo "We are in production, lets not do anything yet"
            secretFileName = "MY_SECRET_FILE_INT"
            currentBuild.displayName =  currentBuild.displayName + " INT"
          } else {
            echo "We are in at Gologic or in DEV"
            secretFileName = "MY_SECRET_FILE"
            currentBuild.displayName =  currentBuild.displayName + " DEV"
          }
          if (env.TAG_NAME) {
            currentBuild.displayName = "Tag ${env.TAG_NAME}"
          } else {
            if (env.CHANGE_AUTHOR) {
              currentBuild.displayName = "Author ${env.CHANGE_AUTHOR}"
            } else {
              currentBuild.displayName = "On ${env.NODE_NAME}"
            }
          }
        }
      }
    }
    stage('Build') {
      steps {
        sh "npm install documentation"
      }
    }
  }
}
