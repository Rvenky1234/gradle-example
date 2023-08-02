pipeline {
     agent any
     stages {
         stage('Clean Workspace') {
             steps {
                  deleteDir()                  
             }
         }
         stage('Clone Project') {
             steps {                  
                  checkout scm                  
             }
         }
          stage ('JDK_11') {
             tools {
               jdk 'java'
          }
             steps{
               sh '''
               java -version
               '''
          }
          }
         stage('Build') {
         tools {
           jdk 'java'
           gradle 'Gradle'
  }
             steps {                  
                  sh "./gradlew shadowJar --debug"
             }              
         }
stage('Docker stage') {
steps {
echo "Building image"
sh 'docker build -t images .'   
}
}
stage('Docker push') {
      steps {
        sh'''
          docker login  --username rvenkat1234 --password Venky@007
          docker tag images:latest rvenkat1234/cloudbackup1234:${version_NUMBER}
          docker push rvenkat1234/cloudbackup1234:${version_NUMBER}
        '''
      }
     }
     }
 }
