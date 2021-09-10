pipeline {
  agent { node { label 'dcs-jenkins_72_host2' } }
  stages {
    stage('Hello') {
      steps {
        echo "hello from Jenkinsfile"
      }
    }
    stage('Try a Job') {
      build job: 'GdummyTest'
    }
  }
}
