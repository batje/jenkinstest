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
          /**
           *
           This should probably be a function in a library
           We are going to figure out what the current context is

           The rules are as follows:

           If we are on master *and* this is a tag build (meaning, we just
           pushed a tag), then we are releasing to PROD

           If we are on master, and this is not a tag build, we are on INT

           If we are on any other branch than master, this is TEST

           We are never on DEV, that is where we connect with our Talend Studio

          */


          if ()(env.BRANCH_NAME == "master") && (env.TAG_NAME)) {

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
          def data = [
            url: "http",
            namespace: "emea.corpdir.net",
            user: "REBATTE",
            password: "tralala",
            debug: false
          ]

          //two alternatives to write

          //native pipeline step:
          writeJSON(file: 'CustomSettings.json', json: data)          
        }
      }
    }
    stage('Build') {
      agent {
        label "cognos && ${Context}"
      }
      when {

      }


      steps {
        sh "npm install babel"
      }
    }
  }
}
