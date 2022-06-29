pipeline {
    agent any
    environment{
	    //it uses id stored in manage creds
        DOCKERHUB_CREDS = credentials('dockerhub')
    }
    stages {
        stage('Clone Repo') {
            steps {
                checkout scm
                sh 'ls *'
            }
        }
        stage('Build Image') {
            steps {
                //sh 'docker build -t raj80dockerid/jenkinstest ./pushdockerimage/' (this will use the tag latest)
		sh 'docker build -t bharath792/jenkinstest:$BUILD_NUMBER ./pushdockerimage/'
            }
        }
        stage('Docker Login') {
            steps {
                sh 'docker login -u 'bharath792' -p 'killermode'
                //sh 'echo $DOCKERHUB_CREDS_PSW | docker login -u $DOCKERHUB_CREDS_USR --password-stdin'                
                }
            }
        stage('Docker Push') {
            steps {
		//sh 'docker push raj80dockerid/jenkinstest' (this will use the tag latest)    
                sh 'docker push bharath792/jenkinstest:$BUILD_NUMBER'
                }
            }
        }
    post {
		always {
			sh 'docker logout'
		}
	 }
    }

