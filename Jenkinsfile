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

  parameters {
    choice(
      name: 'choices', 
      choices: ['deploy blue', 'deploy green', 'switch traffic', 'rollout blue'], 
      description: 'pick one'
    )
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

//     stage('Execute kubectl Command') {
//       steps {
//         container('kubectl') {
//           script {
//             if (params.choices == 'deploy blue') {
//               sh 'kubectl apply -f deploy-blue.yaml'
//               sh 'kubectl apply -f svc-prod.yaml'
//             } else if (params.choices == 'deploy green') {
//               sh 'kubectl apply -f deploy-green.yaml'
//               sh 'kubectl apply -f svc-dev.yaml'
//             } else if (params.choices == 'switch traffic') {
//               sh 'kubectl -n jenkins patch svc demo-blue-svc -p "{\"spec\":{\"selector\":{\"app\":\"demo-green\"}}}"'
//             } else if (params.choices == 'rollout blue') {
//               sh 'kubectl -n jenkins patch svc demo-blue-svc -p "{\"spec\":{\"selector\":{\"app\":\"demo-blue\"}}}"'
//             } else {
//               echo "No valid choice selected."
//             }
//           }
//         }
//       }
//     }
//   }
  }
}
