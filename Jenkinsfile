pipeline {
	agent any
	stages {
		stage('Source') { 
			steps {
				checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/RICHASHRI2211/jenkins2-course-spring-boot.git']]])
			      }
				}
		stage('Build') { 
			tools {
				jdk 'JDK8'
				maven 'Maven'
			      }
			steps {

				// maven build
	    			  powershell label: '', script: 'mvn -f spring-boot-samples/spring-boot-sample-atmosphere/pom.xml clean package'
      
			      }
			}
		
		
		stage('Deploy') {
			steps{
				echo "Deploying"
				deploy adapters: [tomcat7(credentialsId: 'bcff19b9-c8db-470d-b20c-7c8157b5dcb4', path: '', url: 'http://localhost:8085')], contextPath: 'happytrip', war: '**/*.war'
				}
		}
		
		  stage('SonarQube analysis') {
			  steps{
				
					  def scannerHome = tool 'SonarQubeScanner';
  					  withSonarQubeEnv('SonarQube') { 
    					  bat "${scannerHome}/bin/sonar-scanner.bat" 
					  
				  //def mvnHome = tool name: 'Maven', type 'maven'
			  	//withSonarQubeEnv('SonarQube') {
    				//sh 'mvn clean package sonar:sonar'
					  }
							
			  } 
 		 }

		stage('Email Notification'){
			steps{
				mail bcc: '', body: '''Dear Team,

				Build is given.

				Regards,
				Jenkins''', cc: '', from: '', replyTo: '', subject: 'Project happy trip - Build Status', to: 'richa.shrivastava@pratian.com'
			   }
		}
		
	}
}
