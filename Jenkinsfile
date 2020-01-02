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
				//powershell 'java -version'
				//powershell 'mvn -version'
				//powershell 'mvn clean package'

				// maven build
	      powershell label: '', script: 'mvn -f spring-boot-samples/spring-boot-sample-atmosphere/pom.xml clean package'
      
			}
		}
		/*
		stage('Deploy') {
			steps{
				echo "Deploying"
				deploy adapters: [tomcat7(credentialsId: 'bcff19b9-c8db-470d-b20c-7c8157b5dcb4', path: '', url: 'http://localhost:8085')], contextPath: 'happytrip', war: '**/*.war'
				
			}
		}
		*/
	}
}
