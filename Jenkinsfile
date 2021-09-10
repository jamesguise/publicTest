pipeline {
  agent { node { label 'dcs-jenkins_72_host2' } }
  stages {
    stage('Hello') {
      steps {
        echo "hello from Jenkinsfile"
        echo "hello from Trey"
      }
    }
    stage('Try a Job') {
      steps {
        build job: 'GdummyTest'
      }
    }
    stage('Try a MultiJob') {
      steps {
        // build job: 'MultiJob-Guise-test'
        echo "MultiJob done"
      }
    }
    stage('Get PR info') {
      steps {
        if (env.BRANCH_NAME.startsWith('PR-')) {
          def prNum = env.BRANCH_NAME.replace(/^PR-/, '')
          echo prNum
        }
      }
    }
  }
}
