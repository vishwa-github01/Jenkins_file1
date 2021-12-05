

pipeline {
  agent any
   stages {
      stage ("build") {
       steps {
        echo 'This is the Build Stage'
       }
    }

    stage ("test") {
      when {
        expression {
          env.BRANCH_NAME == 'dev1' || env.BRANCH_NAME == 'main'
        }
      }
       steps {
        echo "This is the test Stage"
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
