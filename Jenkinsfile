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
             sh " ssh -i/home/ubuntu/id_rsa ubuntu@172.31.42.68 curl -m 2 http://localhost"
        }

             stage('Deployment Ubuntu node 2') {
              sh """ ssh -i/home/ubuntu/id_rsa ubuntu@172.31.33.132 docker pull registry.hub.docker.com/jogendrajangid/testing
                     ssh -i/home/ubuntu/id_rsa ubuntu@172.31.33.132 docker service update --image registry.hub.docker.com/jogendrajangid/testing php-nginx-frontend
                """
              }    

      stage ('Application health check - Ubuntu node 3') {
             sh " ssh -i/home/ubuntu/id_rsa ubuntu@172.31.33.132 curl -m 2 http://localhost"
        }

             stage('Deployment Ubuntu node 3') {
              sh """ ssh -i/home/ubuntu/id_rsa ubuntu@172.31.47.97 docker pull registry.hub.docker.com/jogendrajangid/testing
                     ssh -i/home/ubuntu/id_rsa ubuntu@172.31.47.97 docker service update --image registry.hub.docker.com/jogendrajangid/testing php-nginx-frontend
                """
              }    

      stage ('Application health check - Ubuntu node 3') {
             sh "ssh -i/home/ubuntu/id_rsa ubuntu@172.31.47.97 curl -m 2 http://localhost"
        }
    }
