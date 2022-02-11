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
            withCredentials([string(credentialsId: 'sanket', variable: 'pass')]) {
             sh "docker login -u shahsanketdocker -p ${pass}"
             sh "docker push shahsanketdocker/repo1:${BUILD_ID}"
            }  
           
          }
       }
       stage("K8s Deployment"){
          steps{
             sh "chmod +x myscript.sh"
             sh " sh myscript.sh ${BUILD_ID}" 
             sshagent(['ubuntu']) {
                 sh "scp -o StrictHostKeyChecking=no  newdep.yaml ubuntu@13.126.114.251:/home/ubuntu"
                 script{
                   try{
                      sh "ssh ubuntu@13.126.114.251 kubectl create -f newdep.yaml"
                   }
                   catch(error){
                        sh "ssh ubuntu@13.126.114.251 kubectl apply -f newdep.yaml"
                   }
                
                 }
             }           
            
          }
       }
 
    }  

}
