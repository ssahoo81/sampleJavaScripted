node {
   stage("build") {
       snDevOpsStep 'a453b4cd9f033300c0745c20942e7051'
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
       snDevOpsStep 'a853b4cd9f033300c0745c20942e7051'
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
       snDevOpsStep '2853b4cd9f033300c0745c20942e7051'
       snDevOpsChange()
       stage("deploy-nested") {
         echo "Deploying"
         sleep 7
       }
   }
}