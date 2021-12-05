

pipeline {
  agent any
  environment {
    // make variable dynamic extract from POM file
    // there variables can be used in any stage
    NEW_VERSION = '1.0.9'
    SERVER_CREDENTIAL = credentials('ID_of the credentials')  // credentials binding plugin need to be installed
    //to bind credentials from jenkins to our env variable
  }
   stages {
      stage ("build") {
       steps {
        echo 'This is the Build Stage'
       }
    }

    stage ("test") {
      when {
        expression {
          // condition of expression to run stage if this condition is met
          env.BRANCH_NAME == 'dev1' || env.BRANCH_NAME == 'main'
          // env.BRANCH_NAME == 'dev1' && <another condition> // and condition
        }
      }
       steps {
        echo "This is the test Stage"
        echo "deploying with credentials ${SERVER_CREDENTIALS}"
        SH "${SERVER_CREDENTIALS}"

        // ELSE  use SERVER_CREDENTIALS
        withCredentials([
          usernamePassword(credentials: ID_of the credentials , usernameVariable: USER , passwordVariable: PWD )
          ])
       }
    }

    stage ("Deploy") {
       steps {
        echo "This is the Deploy Stage"
       }
    }
  }

  post {
    always {
    // Always after the stages are runned
    echo 'Always-post section is running'
    }
    success {
      echo 'Success-post section is running '
    }

    failure {
      echo 'Failure is running only for failure'
    }
  }
}
