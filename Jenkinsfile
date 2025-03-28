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
        publishChecks name: 'Status Reporter', status: 'IN_PROGRESS', title: 'Status Reporter'
        echo "Building.."
        sh '''
          pip install -r ./myapp/requirements.txt
          '''
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
      publishChecks(name: "Build Succeeded")
    }
    failure {
      publishChecks(name: "Build Failed", conclusion: "FAILURE")
    }
  }
}
