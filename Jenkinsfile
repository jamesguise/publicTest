pipeline {
  agent { node { label 'dcs-jenkins_72_host2' } }
  stages {
    stage('Hello') {
      steps {
        echo "hello from Jenkinsfile"
      }
    }
    stage('Try a Job') {
      steps {
        build job: 'GdummyTest'
      }
    }
    stage('Try a MultiJob') {
      steps {
        build job: 'MultiJob-Guise-test'
        echo "MultiJob done"
      }
    }
    stage('Get PR info') {
      steps {
        echo env.CHANGE_ID
      }
    }
  }
}
