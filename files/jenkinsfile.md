<h4 style="text-transform: none;"> Jenkinsfile</h4>


```groovy
// Declarative //
pipeline {
    agent { 
        label 'docker-windows'
    }
    stages {
        
        stage('Build') {
            steps {                
                // Restore Packages and Build Application
            }
        }

        stage('Unit Test') {
            steps {
                // Run Unit Test
            }
        }

        stage('Build Docker Image') {

            steps {
                // Build Docker Image
            }
        }
        
        stage('Push Docker Image') {
            
            steps { 
                // Push Docker Image to Repository
            } 
        }

        stage('Deploy To Canary') {
            
            steps {
                // Deploy to canary server
            }
        }

        stage('Deploy?') {
            steps {
                // Yes o No Deploy to Production Server
            }
        }
    }
}
```