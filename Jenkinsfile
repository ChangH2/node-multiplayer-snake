node ('Ubuntu-app-agent'){  
    def app
    stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */
       checkout scm
    } 
    
    stage('SAST'){
        build 'SECURITY-SAST-SNYK'
    }
    
    
    stage('Build-and-Tag') {
    /* This builds the actual image; synonymous to
         * docker build on the command line */
        app = docker.build("letsgetit/snake")
    }
   
    stage('Post-to-dockerhub') {
        
        sh 'echo test1'
        
        docker.withRegistry('https://registry.hub.docker.com', 'test-id') {
            app.push("latest")
        }
        sh 'echo test2'
    }
      
    stage('SECURITY-IMAGE-SCANNER'){
        build 'SECURITY-IMAGE-SCANNER-AQUAMICROSCANNER'
    }
    
    
    stage('Pull-image-server') {

        
         sh "docker-compose down"
         //sh "docker stop multiplayersnake_snake_1"
         sh "docker-compose up -d"
         sleeop 1000
    }
    
    
    stage('DAST'){
        build 'SECURITY-DAST-OWASP_ZAP'
        //build 'SECURITY-IMAGE-SCANNER-AQUAMICROSCANNER'
    }
    
 
}
