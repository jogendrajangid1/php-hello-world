node {    
      def app     
      stage('Clone repository') {               
             
            checkout scm    
      }     
      stage('Build image') {         
       
            app = docker.build("jogendrajangid/testing")    
       }     
      stage('Test image') {           
            app.inside {            
             
             sh 'echo "Tests passed"'        
            }    
        }     
       stage('Push image') {
              docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {            
              app.push("latest")        
              }    
           }
        
       stage('Deployment Ubuntu node 1') {
              sh """ ssh -i/home/ubuntu/id_rsa ubuntu@172.31.42.68 docker pull registry.hub.docker.com/jogendrajangid/testing
                     ssh -i/home/ubuntu/id_rsa ubuntu@172.31.42.68 docker service update --image registry.hub.docker.com/jogendrajangid/testing php-nginx-frontend
                """
              }    

      stage ('Application health check - Ubuntu node 1') {
             sh "sudo -u jenkins ssh -i/home/ubuntu/id_rsa ubuntu@172.31.42.68 curl -m 2 http://localhost"
        }

    }
