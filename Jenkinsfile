@Library('shared') _
pipeline {
    agent any

    stages {
        stage('Hello Shared'){
            steps{
                script{
                    hello()
                }
            }
        }
        stage('Code') {
            steps {
                sh 'pwd'
                git branch: 'main', url: 'https://github.com/rajan995/django-notes-app.git'
                echo 'Code Pull Successfully'
                sh 'ls'
            }
        }
         stage ('docker login'){
            steps{
                   withCredentials([usernamePassword(credentialsId: 'Docker-hub-crd', passwordVariable: 'PASSWORD', usernameVariable: 'USER')]) {
               echo "Logging in to Docker with user $USER"
               sh 'docker login -u $USER -p $PASSWORD'
}
            }
        }
          stage('Build') {
            steps {
                sh 'docker build -t notes-app:latest .'
                echo 'docker build successfully'
            }
        } 
       
          stage('Push to Docker Hub') {
            steps {
          
               
                sh 'docker tag notes-app:latest rajannagpal99/notes-app:latest'
                sh 'docker push rajannagpal99/notes-app:latest'
                sh 'Docker image push successfully'
            }
        }
          stage('Test') {
            steps {
                echo 'Hello World'
            }
        }
          stage('Run') {
            steps {
                echo 'Hello World'
                sh 'docker compose down && docker compose up -d'
            }
        }
    }
}
