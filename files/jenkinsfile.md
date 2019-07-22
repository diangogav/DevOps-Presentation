<h1 class="title" style="display:none">Jenkinsfile</h1>


```groovy
// Declarative //
def appName = 'app-name'
def feSvcName = "${appName}"
def _IMAGE_TAG = "dockerhub-username/${appName}:${env.BRANCH_NAME}.${env.BUILD_NUMBER}"//

pipeline {
  agent {
    kubernetes {
      label 'sample-app'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  # Use service account that can deploy to all namespaces
  serviceAccountName: cd-jenkins
  containers:
  - name: nodejs
    image: node:latest
    command:
    - cat
    tty: true
  - name: gcloud
    image: gcr.io/cloud-builders/gcloud
    command:
    - cat
    tty: true
  - name: kubectl
    image: gcr.io/cloud-builders/kubectl
    command:
    - cat
    tty: true
"""
}
  }
  stages {
    stage('Restore Packages') {
      steps {
        container('nodejs') {
          sh """
            npm install
          """
        }
      }
    }
    stage('Run Tests') {
      steps {
        container('nodejs') {
          sh """
            npm install jest --save-dev
            npm test
          """
        }
      }
    }
    stage('Build and push image with Container Builder') {
        when {
            expression {
               env.BRANCH_NAME == 'Development' || env.BRANCH_NAME == 'QA' || env.BRANCH_NAME == 'Production' || env.BRANCH_NAME == 'Canary'
            }
        }
        steps {
        container('gcloud') {
          sh "gcloud builds submit --config=cloudbuild.yaml --substitutions=_IMAGE_TAG=${_IMAGE_TAG},_NODE_ENV=${env.BRANCH_NAME} ."
        }      
      }
    }
    stage('Deploy To Development') {
      when { branch "Development" }
      steps{
        container('kubectl') {
          sh("kubectl --namespace=developer apply -f k8s/developer/")
        }
      }
    }
  }
}
```