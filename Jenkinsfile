pipeline {
  agent { 
    node { 
      label 'dcs-jenkins_72_host2'
    } 
  }
  environment {
    TEMP_VAR = 'true'
  }
  stages {
    stage('Check PR Queue') {
      steps {
        publishChecks conclusion: 'NONE', name: 'Jenkins - Check PR Queue', status: 'IN_PROGRESS', summary: 'Checking PR Queue', text: 'need to see if there is a PR', title: 'Check PR Queue'

        sh 'env | sort'
        echo "Check PR Queue . . ."
        
        echo "CHANGE_ID: ${env.CHANGE_ID}"
        echo "CHANGE_TARGET: ${env.CHANGE_TARGET}"
        echo "CHANGE_URL: ${env.CHANGE_URL}"
        echo "CHANGE_TITLE: ${env.CHANGE_TITLE}"
        echo "CHANGE_AUTHOR: ${env.CHANGE_AUTHOR}"
        echo "BRANCH_NAME: ${env.BRANCH_NAME}"
        echo "CHANGE_BRANCH: ${env.CHANGE_BRANCH}"
        echo "BUILD_NUMBER: ${env.BUILD_NUMBER}"
        echo "BUILD_ID: ${env.BUILD_ID}"
        echo "NODE_NAME: ${env.NODE_NAME}"
        echo "JENKINS_URL: ${env.JENKINS_URL}"
        echo "JENKINS_HOME: ${env.JENKINS_HOME}"
        echo "JOB_NAME: ${env.JOB_NAME}"
        
        publishChecks name: 'Jenkins - Check PR Queue', summary: 'Checking PR Queue', text: 'need to see if there is a PR', title: 'Check PR Queue'
      }
    }
    stage('Checkout PR/branch') {
      steps {
        publishChecks conclusion: 'NONE', name: 'Jenkins - Checkout PR/branch', status: 'IN_PROGRESS', summary: 'Checkout PR/branch', text: 'need to checkout a PR/branch', title: 'Checkout PR/branch'
        
        echo "Checked out a PR/branch!"
        
        publishChecks name: 'Jenkins - Checkout PR/branch', summary: 'Checkout PR/branch', text: 'need to checkout a PR/branch', title: 'Checkout PR/branch'
      }
    }
    stage('Build csi-driver') {
      steps {
        script {
          publishChecks conclusion: 'NONE', name: 'Jenkins - Build csi-driver', status: 'IN_PROGRESS', summary: 'Build csi-driver', text: 'need to build csi-driver', title: 'Build csi-driver'
        
          if (env.CHANGE_ID) {
            echo 'FOUND A PR!!!'
            echo "CHANGE_ID: ${env.CHANGE_ID}"
            echo "CHANGE_TARGET: ${env.CHANGE_TARGET}"
            echo "CHANGE_URL: ${env.CHANGE_URL}"
            echo "CHANGE_TITLE: ${env.CHANGE_TITLE}"
            echo "CHANGE_AUTHOR: ${env.CHANGE_AUTHOR}"
            echo "BRANCH_NAME: ${env.BRANCH_NAME}"
            echo "CHANGE_BRANCH: ${env.CHANGE_BRANCH}"
            echo "BUILD_NUMBER: ${env.BUILD_NUMBER}"
            echo "BUILD_ID: ${env.BUILD_ID}"
            
            echo 'Build csi-driver . . .'
            
            publishChecks name: 'Jenkins - Build csi-driver', summary: 'Build csi-driver', text: 'need to build csi-driver', title: 'Build csi-driver'
          }
        }
      }
    }
    stage('Run csi-driver tests') {
      steps {
        build job: 'GdummyTest', parameters: [gitParameter(name: 'upstreamPR', value: '${env.BRANCH_NAME}')]
        echo 'Run csi-driver tests . . .'
      }
    }
    stage('Try a MultiJob') {
      steps {
        build job: 'MultiJob-Guise-test'
        echo "MultiJob done"
      }
    }
    stage('Get PR info') {
      when {
        allOf {
          expression { env.CHANGE_ID != null }
          expression { env.CHANGE_TARGET != null }
        }
      }
      steps {
        echo "All of the expressions were met!"
      }
    }
  }
}
