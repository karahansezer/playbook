pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: ansible
    image: willhallonline/ansible:latest
    command:
    - cat
    tty: true
  """
    }
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install Kubernetes Python Module') {
      steps {
        container('ansible') {
          sh '''
          pip install kubernetes
          '''
        }
      }
    }

    stage('Run Ansible Playbook') {
      steps {
        container('ansible') {
          sh 'ansible-playbook deploy.yml'
        }
      }
    }
  }
}
