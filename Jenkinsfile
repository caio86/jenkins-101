pipeline {
  agent any
  triggers {
    pollSCM "H/1 * * * *"
  }
  stages {
    stage('Build') {
      steps {
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
}
