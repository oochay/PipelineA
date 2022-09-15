pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M2_HOME"
    }

    stages {
        stage('GIT CHECKOUT') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/oochay/PipelineA.git'
            }
        }
        stage('MAVEN BUILD') {
            steps {
                // Get some code from a GitHub repository
                sh "mvn clean install package"
            }
        }
        stage('DOCKER BUILD') {
            steps {
                // Get some code from a GitHub repository
                sh "docker build -t oochay/app_maven_001 ."
            }
        }
        stage('DOCKER PUSH') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker', passwordVariable: 'pwd', usernameVariable: 'user')]) {
                   sh  "docker login -u ${user} -p ${pwd}"
                   sh "docker push apotieri/app_maven_001"
                    }                    
            }
        }
        stage('DOCKER DEPLOY') {
            steps {
            sshagent(['asdasdasd']) {
                                sh "scp -r -o StrictHostKeyChecking=no hellowhale.yaml ubuntu@34.229.50.194:/home/ubuntu"
                script{
						try{
							sh "ssh ubuntu@34.229.50.194 kubectl apply -f ."

							}catch(error)
							{
                            sh "ssh ubuntu@34.229.50.194 kubectl create -f ."
							}
					}
        }
            }
        }
    }
}
