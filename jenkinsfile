pipeline {
    agent any
#    environment {
#        PROJECT_ID = '<<Your GCP Project ID>>'
#        CLUSTER_NAME = '<<Your GKE Cluster Name>>'
#        LOCATION = '<<Your GKE Cluster Location>>'
#        CREDENTIALS_ID = 'multi-k8s'
#   }
    stages {
        stage("Checkout code") {
            steps {
                checkout scm
            }
        }
        stage("Build image") {
            steps {
                script {
                    myapp = docker.build("majdi14/hello:${env.BUILD_ID}")
                }
            }
        }
        stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerID') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }        
 #       stage('Deploy to GKE') {
 #           steps{
 #               sh "sed -i 's/hello:latest/hello:${env.BUILD_ID}/g' deployment.yaml"
 #               step([$class: 'KubernetesEngineBuilder', projectId: env.PROJECT_ID, clusterName: env.CLUSTER_NAME, location: env.LOCATION, manifestPattern: 'deployment.yaml', credentialsId: env.CREDENTIALS_ID, verifyDeployments: true])
 #          }
 #       }
    }    
}
