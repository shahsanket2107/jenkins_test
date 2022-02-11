pipeline {
  agent any
    stages{
       stage("Build Docker Image"){
           steps{
             sh "docker build -t shahsanketdocker/repo1:${BUILD_ID} ."
          }
       }
       stage("Push Image to Repo"){
          steps{
            withCredentials([string(credentialsId: 'dhpass', variable: 'pass')]) {
             sh "docker login -u shahsanketdocker -p ${pass}"
             sh "docker push shahsanketdocker/repo1:${BUILD_ID}"
            }  
           
          }
       }
 
    }  

}
