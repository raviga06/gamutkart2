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
                junit 'target/**/*.xml'
            }
        }

        stage('Deployment') {
            steps {
                sh 'sshpass -p "1234" scp target/gamutkart.war gagan@172.17.0.2:/home/gagan/tomcat/apache-tomcat-9.0.87/webapps'
                sh 'sshpass -p "1234" ssh gagan@172.17.0.2 "/home/gagan/tomcat/apache-tomcat-9.0.87/bin/startup.sh"'
            }
        }
    }
}
