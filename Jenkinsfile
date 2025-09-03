pipeline {
    agent any

    stages {
         stage('Checkout') {
            steps {
                git url: 'https://github.com/Himanshu31bisht/Weather-app.git', branch:'main'
            }
        }
        
        stage('Build Docker Image') {
            steps{
            sh 'docker build . -t himanshu31bisht/weather:latest'
         }
        }

         stage('Push'){
        steps{
           withCredentials([usernamePassword(
                    credentialsId:"dockerHub",
                    usernameVariable:"dockerHubUser",
                    passwordVariable:"dockerHubPass")]){
                 sh 'echo $dockerHubPass | docker login -u $dockerHubUser --password-stdin'
                sh "docker push ${env.dockerHubUser}/weather:latest"
                
                }
         }
         }
         stage('Test'){
         steps{
            echo "Testing the new Build.."
        }
    }
    
     stage('Deploy'){
         steps{
            sh "docker-compose down && docker-compose up -d"
        }
      }
   }
  }


