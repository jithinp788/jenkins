pipeline {
    agent any
	
	  tools
    {
       maven "Maven3"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master',credentialsId: 'github', url: 'https://github.com/jithinp788/jenkins.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp jithinp788/samplewebapp:latest'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'docker push jithinp788/samplewebapp:latest'
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 jithinp788/samplewebapp"
 
            }
        }
// stage('Run Docker container on remote hosts') {
//             
//            steps {
//                sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 nikhilnidhi/samplewebapp"
 //
//            }
   //     }
    }
	}
    
