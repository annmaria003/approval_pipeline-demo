pipeline {
  agent any
  stages {
    
    stage ('Checkout') {
      steps {
        echo 'Pulling code from Github'
        checkout scm
      }
    }

    stage ('Build') {
      steps{
        echo 'Building projects is going on'
        bat 'echo Build completed successfully!'
      }
    }

    stage ('Validation Check') {
      steps {
        echo 'Validating project readiness'
        bat '''
        findstr READY=true check.txt > nul
        if errorlevel 1 (
              echo Validation Failure
              exit 1
        ) else (
              echo Validation Passed
        )
        '''
      }
    }

    stage ('Manager Approval') {
      steps {
        input message: 'Approve Deployment?' , ok: 'Approve'
      }
    }

    stage ('Ready for Deployment') {
      steps {
        echo 'Deployment approved and ready'
      }
    }
    
  } 
}
