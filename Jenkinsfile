//stage 'Build'

node ('Ubuntu-app-agent'){  
    def app
   
    try {
        notifyBuild('STARTED')
        
       stage('Cloning Git') {
            /* Let's make sure we have the repository cloned to our workspace */
            checkout scm
           
       } 
    
        stage('SAST'){
            //build 'SECURITY-SAST-SNYK'
        }
    
    
        stage('Build-and-Tag') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
            app = docker.build("letsgetit/snake")
        }
   
        stage('Post-to-dockerhub') {
        
            
        
            docker.withRegistry('https://registry.hub.docker.com', 'test-id') {
                app.push("latest")
            }
        
        }
      
        stage('SECURITY-IMAGE-SCANNER'){
            //build 'SECURITY-IMAGE-SCANNER-AQUAMICROSCANNER'
        }
    
    
        stage('Pull-image-server') {

        
            //sh "docker-compose down"
            //sh "cd /home/appserver/app-test/node-multiplayer-snake" 
            //sh "docker stop nodemultiplayersnake_snake_1"
            //sh "docker stop multiplayersnake_snake_1" 
            //sh "docker-compose up -d"
      
        }
    
    
        stage('DAST'){
            //build 'SECURITY-DAST-OWASP_ZAP'
        }
    } catch (e) {
        currentBuild.result = "FAILED"
        
        throw e
    } finally {
        notifyBuild(currentBuild.result)
    }
}

def notifyBuild(string buildStatus = 'STARTED') {
    
    // build status of null means successful
    buildStatus = buildStatus ?: 'SUCCESSFUL'
    
    //default values
    
    def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
    
    def summary = "${subject} (${env.BUILD_URL})"
    
    def details = """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at "<a href="${env.BUILD_URL}">${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>"</p>"""
    
    
    // send notifications
    emailext (
        subject: subject,
        
        body : detail,
            mimeType: 'text/html',
        
        // recipentProviders: [[$class: 'DevelopersRecipientProvider']]
            to: 'gusgh1203@gmail.com'
    )
    */
 
}
