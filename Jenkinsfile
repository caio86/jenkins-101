pipeline {
  agent {
    label "python-jenkins-agent"
  }
  triggers {
    pollSCM "H/5 * * * *"
  }
  stages {
    stage('Build') {
      steps {
        withChecks(name: 'Jenkins CI', status: 'IN_PROGRESS') {
          echo "Building.."
          sh '''
            pip install -r ./myapp/requirements.txt
            '''
        }
      }
    }
    stage('Test') {
      steps {
        echo "Testing.."
        sh '''
          python3 myapp/hello.py
          python3 myapp/hello.py --name=Brad
          '''
      }
    }
    stage('Deliver') {
      steps {
        echo 'Deliver....'
        sh '''
          echo "doing delivery stuff.."
          '''
      }
    }
  }
  post {
    success {
      withChecks(name: 'Jenkins CI', status: 'COMPLETED', conclusion: 'SUCCESS')
    }
    failure {
      withChecks(name: 'Jenkins CI', status: 'COMPLETED', conclusion: 'FAILURE')
    }
  }
}
