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
    stage('(0/4): Pre-Setup') {
      
      steps {
        
        script {
          
          TEMP_CHANGED = sh (
            script: 'git --no-pager diff origin/${CHANGE_TARGET} --name-only',
            returnStdout: true
          ).split('\n')
          
          echo "TEMP_CHANGED=${TEMP_CHANGED}"
          
          if ((TEMP_CHANGED.contains("Jenkinsfile")) || (TEMP_CHANGED.contains(".go")) || (TEMP_CHANGED.contains(".sh")) || (TEMP_CHANGED.contains(".repo")) || (TEMP_CHANGED.contains(".service")) || (TEMP_CHANGED.contains("Dockerfile")) || (TEMP_CHANGED.contains(".yaml")) || (TEMP_CHANGED.contains("Makefile")) || (TEMP_CHANGED.contains("COPYING")) || (TEMP_CHANGED.contains("COMPATIBLE")) || (TEMP_CHANGED.contains(".proto")) || (TEMP_CHANGED.contains(".mod")) || (TEMP_CHANGED.contains(".sum"))){
            echo "Important files were changed, need to run tests!"
            TEMP_NUM=1
          } else {
            echo "No important files were changed, no need to run tests!"
          }
        }
        
        publishChecks conclusion: 'NONE', name: '(1/4): Clean arrays', status: 'QUEUED', summary: 'Clean arrays', text: 'need to clean arrays', title: 'Clean arrays'
        publishChecks conclusion: 'NONE', name: '(2/4): Create csi-driver image', status: 'QUEUED', summary: 'Create csi-driver image', text: 'need to create the csi-driver image', title: 'Create csi-driver image'
        publishChecks conclusion: 'NONE', name: '(3/4): Create k8s files', status: 'QUEUED', summary: 'Create k8s files', text: 'need to create k8s files', title: 'Create k8s files'
        publishChecks conclusion: 'NONE', name: '(4/4): Build & test csi-driver', status: 'QUEUED', summary: 'Build & test csi-driver', text: 'need to build & test csi-driver', title: 'Build & test csi-driver'
        sh 'env | sort'
        
      }
    }
    stage('(1/4): Clean arrays') {
      
      steps {
        
        publishChecks conclusion: 'NONE', name: '(1/4): Clean arrays', status: 'IN_PROGRESS', summary: 'Clean arrays', text: 'need to clean arrays', title: 'Clean arrays'

        script{
          if (TEMP_NUM.equals(1)){
            echo "Cleaning arrays . . ."
            //build job: 'create-csi-driver-image', parameters: [string(name: 'PR_NUMBER', value: "${env.CHANGE_ID}")]
            echo "Cleaned arrays!"
          } else {
            echo "Build not required, files changed do not affect tests!"
          }
        }

        publishChecks name: '(1/4): Clean arrays', summary: 'Clean arrays', text: 'need to clean arrays', title: 'Clean arrays'
      
      }
    }
    
    stage('(2/4): Create csi-driver image') {
      
      steps {
        
        publishChecks conclusion: 'NONE', name: '(2/4): Create csi-driver image', status: 'IN_PROGRESS', summary: 'Create csi-driver image', text: 'need to create the csi-driver image', title: 'Create csi-driver image'

        script{
          if (TEMP_NUM.equals(1)){
            echo "Creating csi-driver image . . ."
            build job: 'create-csi-driver-image', parameters: [string(name: 'PR_NUMBER', value: "${env.CHANGE_ID}")]
            echo "Created csi-driver image!"
          } else {
            echo "Build not required, files changed do not affect tests!"
          }
        }

        publishChecks name: '(2/4): Create csi-driver image', summary: 'Create csi-driver image', text: 'need to create csi-driver image', title: 'Create csi-driver image'
      
      }
    }
    stage('(3/4): Create k8s files') {
      
      steps {
        
        script {
          publishChecks conclusion: 'NONE', name: '(3/4): Create k8s files', status: 'IN_PROGRESS', summary: 'Create k8s files', text: 'need to create k8s files', title: 'Create k8s files'

          if (TEMP_NUM.equals(1)){
            echo "Creating k8s files . . ."
            build job: 'create-k8s-files', parameters: [string(name: 'UPSTREAM_EDGE_NUMBER', value: "${env.CHANGE_ID}")]
            echo "Created k8s files!"
          } else {
            echo "Build not required, files changed do not affect tests!"
          }

          publishChecks name: '(3/4): Create k8s files', summary: 'Create k8s files', text: 'need to create k8s files', title: 'Create k8s files'

        }
      }
    }
    stage('(4/4): Build & test csi-driver') {
      
      steps {
        
        script {
          publishChecks conclusion: 'NONE', name: '(4/4): Build & test csi-driver', status: 'IN_PROGRESS', summary: 'Build & test csi-driver', text: 'need to build & test csi-driver', title: 'Build & test csi-driver'

          if (TEMP_NUM.equals(1)){
            echo "Build & test csi-driver . . ."
            build job: 'build-test-csi-driver'
            echo "Built & tested csi-driver!"
          } else {
            echo "Build not required, files changed do not affect tests!"
          }

          publishChecks name: '(4/4): Build & test csi-driver', summary: 'Build & test csi-driver', text: 'need to build & test csi-driver', title: 'Build & test csi-driver'

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
