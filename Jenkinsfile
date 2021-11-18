pipeline {
    
    agent any
    
    tools {
        maven "maven"
        }
    stages {
	stage('build') {
            steps {
                sh "mvn package"
            }
	}
	stage('Sonar Scan') {
            steps {
                sh "echo 'Passed Sonar Quality Scan '"
            }
	}
	stage('Publish Artifacts') {
            steps {
                sh "echo 'Published Artifacts Artifactory'"
            }
	}
	stage('Deploy to Dev') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'tomcatcreds', path: '', url: 'http://3.121.211.98:8081/')], contextPath: '/', war: 'target/*.war'
            }
	}
	stage('Approve') {
            steps {
                timeout(time: 10, unit: 'MINUTES') {
        	input message: "Click on Proceed to Deploy to QA? "
            }
	}
	stage('Deploy to QA') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'tomcatcreds', path: '', url: 'http://3.121.211.98:8082/')], contextPath: '/', war: 'target/*.war'
            }
	}



    }
	post {
        always {          
            archiveArtifacts artifacts: "**/target/*.war", onlyIfSuccessful: true
            
  
        }
    }
}
