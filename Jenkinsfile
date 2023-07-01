pipeline {
    agent {
        kubernetes {
            yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
  - name: ansible
    image: willhallonline/ansible:latest
    command:
    - cat
    tty: true
  volumes:
  - name: kubeconfig
    hostPath:
      path: /home/karahan/.kube/config
  serviceAccount: jenkins-deployer
"""
        }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                container('ansible') {
                    sh 'ansible-playbook -i localhost, -c local deploy.yml'
                }
            }
        }
    }
}
