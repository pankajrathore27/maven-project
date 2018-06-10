pipeline{
 agent any 
 tools
 {
     jdk 'jdk_8'
     maven 'maven3'
 }
 stages {
     stage('Initilize')
     {
     steps
     {
         echo "this is initilize stage"
         sh '''
          
          echo "PATH=${PATH}"
          echo "M2_HOME=${M2_HOME}"
         sh '''
     }
     }
     stage('bulid stage is now')
     {
     steps
     {
         echo "this is bulid stage "
         sh 'mvn clean package checkstyle:checkstyle'
     }
     post{
         success
         {
                echo "Genrate checkstyle:checkstyle"
                checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
                echo "Genrate junit reports"
                junit '**/target/surefire-reports/*.xml'
                echo " Archive artfacts"
                archiveArtifacts '**/*.war'
                


         }
     }
     }
     stage('final deploy to')
     {
     steps
     {
         echo "now build is deploying to staging"
         build 'deploying-staging'

     }

     }

       stage('final deploy to prod')
     {
     steps
     {

      timeout(2) {
    
              input 'do we allow it for prod'

                 }

         echo "now build is deploying to prod"
         build 'prod'

     }

     }

 }
 

}
