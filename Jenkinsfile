pipeline {
    agent any
    
    tools{
        maven "Maven-3.9.10"
    }    

    stages {
        stage('Git Clone') {
            steps {
               git branch: 'main', url: 'stage('Git Clone') {
    steps {
        git branch: 'main', url: 'https://github.com/Dhatrijanch/01_products_api.git'
    }
}
          }
        }
        stage('Maven Build'){
            steps{
             sh 'mvn clean package'
            }
        }
        stage('Docker Image'){
            steps{
             sh 'docker build -t dhatrinch/products_api .'
            }
        }
        stage('Docker Image push'){
            steps{
            withCredentials([string(credentialsId: 'docker_pwd', variable: 'docker_pwd')]) {
                   sh 'docker login -u dhatrinch -p ${docker_pwd}'
                   sh 'docker push dhatrinch/products_api'
            }
            }
        }
        stage('kubernetes deployment'){
            steps{
             sh 'kubectl apply -f Deployment.yml'
            }
        }        
    }
}
