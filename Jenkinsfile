env.mvnHome = '/usr/share/maven'
node {
   
   
   stage('Preparation') { // for display purposes
      
      git 'https://github.com/rahulgreddy/simple-maven-project-with-tests.git'
        
      
   }
   stage('Build') {
      
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' clean install"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
   }
node{
   stage("update th ecode in master"){
   sh "mco  r10k -f r10k.yml "
   }
   stage('deployment') {
      sh "mco puppetd runonce --server puppet.example.com"
   }

}
