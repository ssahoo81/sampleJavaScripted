node {
   git 'https://github.com/ssahoo81/sampleJavaScripted'
   stage("build") {
       snDevOpsStep '36945e350fb333009d1a986eb4767e22'
       echo "Building" 
         sh 'mvn clean install'        
       sleep 5
       parallel 'build-nested1': {
           stage('build-nestedA') {
               echo "building nested A"
               sleep 3
           }
       }, 'build-nested2': {
           stage('build-nestedB') {
               echo "building nested B"
               sleep 2
           }
       }
   }
   stage("test") {
       snDevOpsStep 'ba945e350fb333009d1a986eb4767e22'
       echo "Testing"
         sh 'mvn test -Dpublish'
       stage("test-nested") {
         echo "Testing nested"
         sleep 7
         stage("test-nestedx2") {
            echo "Testing nested 2"
            sleep 2
         }
       }
       sleep 3
       junit '**/target/surefire-reports/*.xml' 
   }
   stage("deploy") {
       snDevOpsStep '3e945e350fb333009d1a986eb4767e22'
       snDevOpsChange()
       stage("deploy-nested") {
         echo "Deploying"
         sleep 7
       }
   }
}
