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
    stage('Jenkins - Stage 1: Checkout PR') {
      steps {
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 1: Checkout PR', status: 'IN_PROGRESS', summary: 'Checkout PR', text: 'need to checkout a PR', title: 'Checkout PR'
        
        echo "Checked out a PR/branch!"
        sh 'env | sort'
        
        publishChecks name: 'Jenkins - Stage 1: Checkout PR', summary: 'Checkout PR', text: 'need to checkout a PR', title: 'Checkout PR'
      }
    }
    stage('Jenkins - Stage 2: Pre-tasks') {
      steps {
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 2: Pre-tasks', status: 'IN_PROGRESS', summary: 'Checking GO install', text: 'need to see if there is GO installed', title: 'Checking GO install'

        build job: 'GdummyTest', parameters: [string(name: 'upstreamChangeID', value: "${env.CHANGE_ID}")]
        
        publishChecks name: 'Jenkins - Stage 2: Pre-tasks', summary: 'Checking GO install', text: 'need to see if there is GO installed', title: 'Checking GO install'
      }
    }
    stage('Jenkins - Stage 3: Build & test csi-driver') {
      steps {
        script {
          publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 3: Build & test csi-driver', status: 'IN_PROGRESS', summary: 'Build & test csi-driver', text: 'need to build & test csi-driver', title: 'Build & test csi-driver'
        
          build job: 'job-k8s-v.1.18'
          
          publishChecks name: 'Jenkins - Stage 3: Build & test csi-driver', summary: 'Build & test csi-driver', text: 'need to build & test csi-driver', title: 'Build & test csi-driver'
          
        }
      }
    }
    stage('Jenkins - Stage 4: Clear & send results') {
      steps {
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 4: Clear & send results', status: 'IN_PROGRESS', summary: 'Clear & send results', text: 'need to clear & send results', title: 'Clear & send results'
        
        echo "Clearing build & sending results . . ."
        
        publishChecks name: 'Jenkins - Stage 4: Clear & send results', summary: 'Clear & send results', text: 'need to clear & send results', title: 'Clear & send results'
        
      }
    }
  }
}
