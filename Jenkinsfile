pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                sh 'docker build -f dockerfile . -t mahmoudshaaban5/jenkins_iti:latest'
            }
        }
        stage('push') { 
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]){
                sh 'docker login -u ${USERNAME} -p ${PASSWORD} '
                sh 'docker push mahmoudshaaban5/jenkins_iti:latest' 
            }
            }
        }
         stage('deploy') {
     steps {
            sh 'docker rm -f nodejs '
            sh 'docker run -p 3000:3000 -d --name nodejs mahmoudshaaban5/jenkins_iti:latest'
     }
    }
    }
}
