pipeline {
    agent { label 'JDK17' }
  //  environment {
    //   MVN = '/opt/apache-maven-3.9.9/bin/mvn'
 //  }
   // tools {
    //   maven 'MAVEN_HOME'
  //  }
    options { 
        timeout(time: 1, unit: 'HOURS')
        retry(2)
   }
    triggers {
      cron('0 * * * *')
   }
    parameters { 
          choice(name: 'GOAL', choices: ['clean', 'clean package', 'clean install'])
   }
    stages {
       stage('Git clone') {
          steps {
              git url: 'https://github.com/mailrajeshsre/spring-petclinic.git', branch: 'main'
         }
      }
       stage('Build the code') {
         steps {
            sh  "/opt/apache-maven-3.9.9/bin/mvn ${params.GOAL}"
        }
      }
      stage('Reporting and Arhchiving') {
        steps {
           junit testResults : 'target/surefire-reports/*.xml'
        }
      }
 }
   post {
    success {
      //send the success email
      echo "Success"
   }
    unsuccessful {
       //send the unsuccess email
      echo "Failure"
   }
 }
}
