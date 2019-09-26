pipeline {/root/distros/jdk1.8.0_221/bin/java

    agent any

	tools {
		maven 'maven-3.6.2'
	}
	environment {
		M2_HOME ='/root/Distros/apache-maven-3.6.2/bin/mvn'
	}

    stages {
		stage('Clone-Repo') {
			steps {
				checkout scm
			}
		}
		stage('Build') {
	    	steps {
				sh 'mvn install -DskipTests'
			}
	    }
		stage('Unit Tests') {
			steps {
				sh 'mvn surefire:test'
			}
		}
		stage('Deployment') {
	    	steps {
				sh 'sshpass -p "shyam" scp target/gamutkart.war shyam@172.17.0.3:/root/distros/apache-tomcat-8.5.45/webapps
'
				sh 'sshpass -p "shyam" ssh gamut@172.17.0.3 "JAVA_HOME=/root/distros/jdk1.8.0_221/bin/" "/root/distros/apache-tomcat-8.5.45/webapps
/bin/startup.sh"'
	    	}
		}
    }
}
