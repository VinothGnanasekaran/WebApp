pipeline {
  agent any
  stages {
    stage('Dev Code Pull') {
      steps {
        echo 'Dev code pull from Git to Jenkins Workspace is successful'
      }
    }

    stage('Dev Maven Build') {
      steps {
        echo 'Building the Dev Project using Maven - Successful'
        echo 'Build Successful - Email to Dev team'
      }
    }

    stage('QA Deploy') {
      steps {
        echo 'Deployed the Build to QA Environment'
        echo 'Sent an Email trigger To QA Team'
      }
    }

    stage('QA Test ') {
      parallel {
        stage('QA Test Web') {
          steps {
            echo 'QA  Web Code pull from Git'
            echo 'Execute the Web Smoke test - Success'
          }
        }

        stage('QA Test API') {
          steps {
            echo 'QA Test API - Code Pull from Git'
            echo 'Execute REST API Test - successful'
          }
        }

      }
    }

    stage('QA Certify') {
      steps {
        input 'Is Build passed QA  successfully?'
        echo 'QA Certified - Manually'
      }
    }

    stage('UAT Deploy') {
      when {
        branch 'master'
      }
      steps {
        echo 'Build Deployed to UAT Region'
        echo 'Notify the UAT user with email'
      }
    }

    stage('UAT Certify') {
      when {
        branch 'master'
      }
      steps {
        input 'Is UAT Done and Ready to Go for Prod?'
        echo 'UAT Certified - Manually Successful'
      }
    }

    stage('Prod Deploy') {
      when {
        branch 'master'
      }
      steps {
        echo 'Build Successfully Deployed to PROD region - Hurray!!'
      }
    }

  }
}