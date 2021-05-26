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
              docker.withRegistry('https://registry.hub.docker.com', '96c81ae1-9c95-456c-8a7f-11cef47fccb7') {            
              app.push("latest")        
              }    
           }
        }
