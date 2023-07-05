pipeline {
  agent {
    kubernetes {
      yaml '''
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  serviceAccountName: jenkins-deployer
  containers:
  - name: ansible
    image: willhallonline/ansible:latest
    command:
    - cat
    tty: true
  '''
    }
  }
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Deploy to Kubernetes') {
      steps {
        container('ansible') {
          sh 'pip install kubernetes'
          sh 'ansible-galaxy collection install community.kubernetes'
          sh 'ansible-playbook deploy.yml'
        }
      }
    }
  }
}
