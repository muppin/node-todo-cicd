pipeline{
    agent any
    stages{
        stage('Checkout'){
            steps{
                git 'https://github.com/muppin/node-todo-cicd.git'
            }
        }
        stage('Build'){
            steps{
                sh 'docker build -t node_app .'
            }
        }
        stage('Dockerpush'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'pswd', usernameVariable: 'usr')]) {
                 sh 'docker login -u $usr -p $pswd' 
                 sh 'docker tag node_app muppin/node_app:${BUILD_NUMBER}'
                 sh 'docker push muppin/node_app:${BUILD_NUMBER} '
                    
                }
            }
        }
        stage('Deploy'){
            steps{
             sh "docker-compose down && docker-compose up -d"
            
            }
        }
        stage('remove image'){
            steps{
                sh 'docker rmi muppin/node_app:${BUILD_NUMBER}'
            }
        }
    
    }
}     

