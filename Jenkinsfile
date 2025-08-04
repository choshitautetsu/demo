pipeline {
  agent {
    kubernetes {
      cloud 'gke'
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: kubectl
    image: bitnami/kubectl:1.27.4
    command:
    - sleep
    - "3600"
    tty: true
    securityContext:
      runAsUser: 1000
      runAsGroup: 1000
      fsGroup: 1000

"""
    }
  }
  stages {
    stage('Test kubectl') {
      steps {
        container('kubectl') {
          sh 'id'
          sh 'pwd'
        }
      }
    }
  }
}