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
    stage('Jenkins - Stage 2: Build csi-driver') {
      steps {
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 2: Build csi-driver', status: 'IN_PROGRESS', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'

        build job: 'GdummyTest', parameters: [string(name: 'upstreamChangeID', value: "${env.CHANGE_ID}")]
        
        publishChecks name: 'Jenkins - Stage 2: Build csi-driver', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'
      }
    }
    stage('Jenkins - Stage 3: Test csi-driver') {
      steps {
        script {
          publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 3: Test csi-driver', status: 'IN_PROGRESS', summary: 'Testing csi-driver', text: 'need to test csi-driver', title: 'Testing csi-driver'
        
          build job: 'job-guise-csi-test'
          echo "Completed job-guise-csi-test . . ."
          build job: 'job-k8s-v.1.18'
          
          publishChecks name: 'Jenkins - Stage 3: Test csi-driver', summary: 'Testing csi-driver', text: 'need to test csi-driver', title: 'Testing csi-driver'
          
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
