pipeline { 
   environment { 
      registry = "kevinhacoder/achistar_tech" 
      registryCredential = 'kevinhacoder' 
      dockerImage = '' 
   }
   agent any 
   stages { 
      stage('Cloning our Git') { 
         steps { 
            git 'https://github.com/AchiStar-Technologies/JavaRepo.git' 
         }
      } 
      stage('Building Docker Image') { 
         steps { 
            script { 
               dockerImage = docker.build registry + ":$BUILD_NUMBER" 
            }
         } 
      }
      stage('Deploy Docker image') { 
         steps { 
            script { 
               docker.withRegistry( '', registryCredential ) { 
                  dockerImage.push() 
               }
            } 
         }
      } 
      stage('Cleaning up') { 
         steps { 
            sh "docker rmi $registry:$BUILD_NUMBER" 
         }
      } 
   }
}
