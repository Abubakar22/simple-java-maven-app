pipeline {
    agent {
			label 'master'
        }
		
	/*triggers {
        cron('H/2 * * * *')
    } */	
    
    stages {
	
		stage ('checkout') {
			steps {
				checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'Gtihub', url: 'https://github.com/Abubakar22/test-simple-java-maven-app']]])
			}
		}
		
        stage('compile') {
            steps {
                bat 'mvn -B -DskipTests  compile'
            }
        }
		
		stage('Package') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
		
		stage('install') {
            steps {
                bat 'mvn -B -DskipTests install'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
       /* stage('Deliver') {
            steps {
                bat './jenkins/scripts/deliver.sh'
            }
        } */
    }
}
