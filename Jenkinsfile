// Declarative //
pipeline {
  agent any
  stages {
  stage('Git Checkout SCM') {
  steps {
      echo 'Clonando Proyecto'
        sleep(14.45)
      }
  }
  stage('Build') {
      steps {
        echo 'Compilando..'
        sleep(4.65)
      }
  }
  stage('Test') {
      steps {
        echo 'Ejecutando Pruebas....'
        sleep(8.753)
      }
  }
  stage('Build Docker Image') {
      steps {
        echo 'Creando Imagen Docker ....'
        sleep(20.1115)
      }
  }
  stage('Push Docker Image') {
      steps {
        echo 'Guardando Imagen Docker....'
        sleep(10.1110)
      }
  }
  stage('Deploy To Canary') {
      steps {
        echo 'Desplegando en servidor de pruebas....'
        sleep(3.11)
      }
  }
  stage('Deploy?') {
            steps {
                timeout(time:5, unit:'DAYS') {
                    input message:'Approve deployment?', submitter: 'it-ops'
                }
            }
        }
  }
}
