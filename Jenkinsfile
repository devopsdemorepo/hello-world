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
                sh "echo 'Sonar scan'"
            }
	}
	stage('Publish Artifacts') {
            steps {
                sh "echo 'published Artifacts'"
            }
	}
	stage('Deploy to Dev') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'tomcatcreds', path: '', url: 'http://3.121.211.98:8082/')], contextPath: '/', war: 'target/*.war'
            }
	}
	stage('Approve') {
            steps {
                sh "echo 'abc'"
            }
	}
	stage('Deploy to QA') {
            steps {
                sh "echo 'package'"
            }
	}



    }
	post {
        always {          
            archiveArtifacts artifacts: "**/target/*.war", onlyIfSuccessful: true
            
  
        }
    }
}
