node {
   git 'https://github.com/ssahoo81/sampleJavaScripted'
   stage("build") {
       snDevOpsStep '0076b32b0fe333009d1a986eb4767e1a'
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
       snDevOpsStep '8c76b32b0fe333009d1a986eb4767e19'
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
       snDevOpsStep '8476b32b0fe333009d1a986eb4767e19'
       snDevOpsChange()
       stage("deploy-nested") {
         echo "Deploying"
         sleep 7
       }
   }
}
