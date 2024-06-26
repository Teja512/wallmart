pipeline {
    agent any

//	tools {
//		jdk 'jdk8'
//	}
//	environment {
//		M2_INSTALL = "/usr/bin/mvn"
//	}

    stages {
        stage('Clone-Repo') {
	    	steps {
	        	checkout scm
	    	}
        }

        stage('Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }
		
        stage('Unit Tests') {
            steps {
                sh 'mvn compiler:testCompile'
                sh 'mvn surefire:test'
            }
        }

        stage('Deployment') {
            steps {
                sh 'sshpass -p "gamut" scp target/flipkart.war gamut@172.17.0.3:/home/gamut/Distros/apache-tomcat-9.0.78/webapps'
                sh 'sshpass -p "gamut" ssh gamut@172.17.0.3 "/home/gamut/Distros/apache-tomcat-9.0.78/bin/startup.sh"'
            }
        }
    }
}
