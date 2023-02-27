pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                git 'https://github.com/darwish7/app-repo'
                withCredentials([usernamePassword(credentialsId: 'docker-cred', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
                sh """
                docker login -u ${USERNAME} -p ${PASSWORD}
                cd DevOps-Challenge-Demo-Code-master
                docker build -f Dockerfile -t ziad/app:v1 .
                docker push ziad/app:v1
                """
            
            }
            }
            
        }
        stage('CD'){
            steps{
                     withCredentials([usernamePassword(credentialsId: 'docker-cred', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
                sh """
                docker login -u ${USERNAME} -p ${PASSWORD}
                cd kubernetes-yaml-files/
                kubectl apply -f redis-deployment.yml
                kubectl apply -f redis-srvc.yml
                kubectl apply -f python-app.yml
                kubectl apply -f loadBanlancer.yml
                """
                     }
            }
        }
        
    }
}

