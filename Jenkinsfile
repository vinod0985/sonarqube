import jenkins.model.*
pipeline {
   agent any

   stages {
     stage('sonar') {
      steps {
        ansiColor('x-term') {
          script {
            dir("maven-1") {
              docker.withRegistry('https://registry.hub.docker.com', 'demo') {
                docker.image("magalam87/sonar-scanner:v1").inside(){
                withSonarQubeEnv('sonarqube'){
                  sh """
		      ls -lrt
                      sonar-scanner -Dproject.setting=./sonar-project.properties
                      """;
                }
                }
              }
            }
           sleep(10)  
       		 timeout(time: 1, unit: 'HOURS') {
         	 waitForQualityGate abortPipeline: false
        	
      	      }
          }
        }
      }
     }
	      }
   }
