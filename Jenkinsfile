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
        
        
        slackSend channel: '#jenkins-intern-project1', color: "#439FE0", message: "${env.BUILD_TAG}: Successfully ran all tests! Ready to be approved and merged to Master branch! You can view the pipeline outlook: ${env.RUN_DISPLAY_URL}", teamDomain: 'hpe-internal'
        
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 1: Checkout PR', status: 'QUEUED', summary: 'Checkout PR', text: 'need to checkout a PR', title: 'Checkout PR'
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 2: Build csi-driver', status: 'QUEUED', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 3: Test csi-driver', status: 'QUEUED', summary: 'Testing csi-driver', text: 'need to test csi-driver', title: 'Testing csi-driver'
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 4: Clear & send results', status: 'QUEUED', summary: 'Clear & send results', text: 'need to clear & send results', title: 'Clear & send results'
        
        
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 1: Checkout PR', status: 'IN_PROGRESS', summary: 'Checkout PR', text: 'need to checkout a PR', title: 'Checkout PR'
        
        sh 'env | sort'
        echo "Checking out a PR/branch . . ."
        build job: 'job-checkout2', parameters: [string(name: 'upstreamChangeID', value: "${env.CHANGE_ID}")]
        echo "Checked out a PR/branch!"
        
        publishChecks name: 'Jenkins - Stage 1: Checkout PR', summary: 'Checkout PR', text: 'need to checkout a PR', title: 'Checkout PR'
      }
    }
    stage('Jenkins - Stage 2: Build csi-driver') {
      steps {
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 2: Build csi-driver', status: 'IN_PROGRESS', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'

        echo "Building csi-driver . . ."
        build job: 'GdummyTest', parameters: [string(name: 'upstreamChangeID', value: "${env.CHANGE_ID}")]
        echo "Built csi-driver!"
        
        publishChecks name: 'Jenkins - Stage 2: Build csi-driver', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'
      }
    }
    stage('Jenkins - Stage 3: Test csi-driver') {
      steps {
        script {
          publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 3: Test csi-driver', status: 'IN_PROGRESS', summary: 'Testing csi-driver', text: 'need to test csi-driver', title: 'Testing csi-driver'
        
          echo "Testing csi-driver . . ."
          build job: 'job-guise-csi-test'
          echo "Completed job-guise-csi-test . . ."
          build job: 'job-k8s-v.1.18'
          echo "Tested csi-driver!"
          
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
