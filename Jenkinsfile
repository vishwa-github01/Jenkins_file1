

pipeline {
  agent any
  environment {
    // make variable dynamic extract from POM file
    // there variables can be used in any stage
    NEW_VERSION = '1.0.9'
    SERVER_CREDENTIAL = credentials('server-credentials')  // credentials binding plugin need to be installed
    //to bind credentials from jenkins to our env variable
  }
  // tools {
  //   //install glob tools config install maven n ver
  //   maven 'Maven'
  //   gradel
  //   // build tools MAVEN Gradle, yarn etc // sh "mvn install"
  //   // 3 tools support as of now // config tools
  // }
  parameters {
    //parameterise your Build to select values
    // string(name: 'VERSION' , defaultValue: '' , description: 'some description')
    choice(name: 'VERSION' , choices: [ '1.0.9', '1.0.8'] , description: 'some description of choices')
    booleanParam(name: 'executeTest' , defaultValue: true , description: 'some parm description')
  }

   stages {
      stage ("build") {
        when {
          expression {
          // condition to run the stages params
          params.executeTest == true
          }
        }
       steps {
        echo 'This is the Build Stage'
        echo "the param choice of VERSIOn is: ${params.VERSION}"
        echo "the choice of the param execute test is : ${executeTest}"
        echo "This is the env variable ${env.NEW_VERSION}"
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
        echo "deploying with credentials ${env.SERVER_CREDENTIAL}"
        sh "${env.SERVER_CREDENTIAL}"
        echo " server credentials are: ${env.SERVER_CREDENTIAL}"

        // ELSE  use SERVER_CREDENTIAL
        withCredentials([
          usernamePassword(credentials: 'server-credentials' , usernameVariable: 'USER' , passwordVariable: 'PWD' )
          ]) {
            sh """
                 ${USER} ${PWD}
            """
          }
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
