pipeline {
  agent { 
    node { 
      label 'dcs-jenkins_72_host2'
    } 
  }
  environment {
    TEMP_NUM = 5
  }
  stages {
    stage('Jenkins - Stage 0: Pre-Setup') {
      steps {
        echo "TEMP_NUM=${TEMP_NUM}"
        
        //publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 1: Checkout PR', status: 'QUEUED', summary: 'Checkout PR', text: 'need to checkout a PR', title: 'Checkout PR'
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 1: Build csi-driver', status: 'QUEUED', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 2: Build k8s files', status: 'QUEUED', summary: 'Building k8s files', text: 'need to build k8s files', title: 'Building k8s files'
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 3: Test csi-driver', status: 'QUEUED', summary: 'Testing csi-driver', text: 'need to test csi-driver', title: 'Testing csi-driver'
        //publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 5: Clear & send results', status: 'QUEUED', summary: 'Clear & send results', text: 'need to clear & send results', title: 'Clear & send results'

        
        //publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 1: Checkout PR', status: 'IN_PROGRESS', summary: 'Checkout PR', text: 'need to checkout a PR', title: 'Checkout PR'
        
        sh 'env | sort'
        //echo "Checking out a PR/branch . . ."
        //build job: 'job-checkout2', parameters: [string(name: 'upstreamChangeID', value: "${env.CHANGE_ID}")]
        //echo "Checked out a PR/branch!"
        
        //publishChecks name: 'Jenkins - Stage 1: Checkout PR', summary: 'Checkout PR', text: 'need to checkout a PR', title: 'Checkout PR'
      }
    }
    stage('Jenkins - Stage 1: Build csi-driver') {
      steps {
        publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 1: Build csi-driver', status: 'IN_PROGRESS', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'

        echo "Building csi-driver . . ."
        //build job: 'GdummyTest', parameters: [string(name: 'upstreamChangeID', value: "${env.CHANGE_ID}")]
        //build job: 'job-build2', parameters: [string(name: 'upstreamChangeID', value: "${env.CHANGE_ID}")]
        build job: 'job-build3', parameters: [string(name: 'upstreamChangeID', value: "${env.CHANGE_ID}")]
        //build job: 'job-build-test', parameters: [string(name: 'upstreamChangeID', value: "${env.CHANGE_ID}")]
        echo "Built csi-driver!"
        
        sh 'env | sort'
        
        
        publishChecks name: 'Jenkins - Stage 1: Build csi-driver', summary: 'Building csi-driver', text: 'need to build csi-driver', title: 'Building csi-driver'
      }
    }
    stage('Jenkins - Stage 2: Build k8s files') {
      steps {
        script {
          publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 2: Build k8s files', status: 'IN_PROGRESS', summary: 'Building k8s files', text: 'need to build k8s files', title: 'Building k8s files'
        
          echo "Building k8s files . . ."
          //build job: 'job-guise-csi-test'
          //build job: 'job-test3'
          build job: 'csi-driver-PR', parameters: [string(name: 'UPSTREAM_EDGE_NUMBER', value: "${env.CHANGE_ID}"), string(name: 'PR_BUILD_NUMBER', value: "${TEMP_NUM}")]
          //echo "Completed job-guise-csi-test . . ."
          //build job: 'job-k8s-v.1.18'
          echo "Built k8s files!"
          
          echo "TEMP_NUM=${TEMP_NUM}"
          
          publishChecks name: 'Jenkins - Stage 2: Build k8s files', summary: 'Building k8s files', text: 'need to build k8s files', title: 'Building k8s files'
          
        }
      }
    }
    stage('Jenkins - Stage 3: Test csi-driver') {
      steps {
        script {
          publishChecks conclusion: 'NONE', name: 'Jenkins - Stage 3: Test csi-driver', status: 'IN_PROGRESS', summary: 'Testing csi-driver', text: 'need to test csi-driver', title: 'Testing csi-driver'
        
          echo "Testing csi-driver . . ."
          //build job: 'job-ext-test', parameters: [string(name: 'CSI_BUILD_NUMBER', value: "${TEMP_NUM}")]
          ////build job: 'job-ext-test3'
          echo "Tested csi-driver!"

          
          publishChecks name: 'Jenkins - Stage 3: Test csi-driver', summary: 'Testing csi-driver', text: 'need to test csi-driver', title: 'Testing csi-driver'

        }
     
        slackSend channel: '#jenkins-intern-project1', color: "#17c40e", message: """${env.BUILD_TAG}: Successfully ran all tests!
        Ready to be approved and merged to Master branch!
        Waiting to be reviewed . . .
        You can view the Jenkins Job Pipeline: ${env.JOB_URL}
        You can view the Jenkins Blue Ocean Pipeline: ${env.RUN_DISPLAY_URL}
        You can view the PR on GitHub: ${env.CHANGE_URL}""", teamDomain: 'hpe-internal'
        
      }
    }
  }
}
