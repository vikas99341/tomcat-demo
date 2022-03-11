node {  
    def mvnHome = tool name: 'maven home', type: 'maven'
    stage('SCM-Checkout') { 
        git branch: 'main', credentialsId: 'Git-Credentials', url: 'https://github.com/vikas99341/tomcat-demo.git' 
    }
    stage('mvn-clean') { 
        sh "${mvnHome}/bin/mvn clean"
    }
    stage('mvn-compile') { 
        sh "${mvnHome}/bin/mvn compile"
    }
    stage('mvn-test') { 
        sh "${mvnHome}/bin/mvn test"
    }
    stage('mvn-package') { 
        sh "${mvnHome}/bin/mvn package"
    }
    stage('Tomcat-deployment') { 
        sshagent(['ec2-user']) {
			sh "scp -o StrictHostKeyChecking=no target/tomcat-demo.war ec2-user@172.31.81.9:/opt/tomcat/webapps"
		}
    }
}
