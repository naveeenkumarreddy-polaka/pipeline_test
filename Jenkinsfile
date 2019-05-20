#!groovy

pipeline{
	agent any
	stages{
		stage('git checkout'){
			steps{
				git changelog: false, credentialsId: 'testgit', poll: false, url: 'https://github.com/naveeenkumarreddy-polaka/test.git'
			}
		}
		stage('Sonar Scan'){
			steps{
				bat "mvn sonar:sonar"
			}
		}
		
		

		stage('Build & Artifactory Storage'){
			steps{
				bat "mvn clean deploy"
			}
		}
		stage('Deploy to Tomcat'){
			steps{
				rtDownload (
   					serverId: "Jfrog",
    					spec:
        					"""{
         					  "files": [
           					   {
              					     "pattern": "bazinga-repo/froggy-files/",
              					     "target": "bazinga/,
           					   }
         					]
        					}"""
					)
				
				//bat 'copy "C:\\Program Files (x86)\\Jenkins\\workspace\\test\\target\\*.war" C:\\Users\\qw693\\Documents\\Devops_tools\\apache-tomcat-8.5.40\\webapps'
			}
		}
	}
}
