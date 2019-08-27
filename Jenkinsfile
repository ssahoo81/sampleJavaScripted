node {
   stage("build") {
       snDevOpsStep '241012150fa333009d1a986eb4767efe'
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
       snDevOpsStep '2c1012150fa333009d1a986eb4767efe'
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
       snDevOpsStep '2c1012150fa333009d1a986eb4767efe'
       snDevOpsChange()
       stage("deploy-nested") {
         echo "Deploying"
         sleep 7
       }
   }
}
