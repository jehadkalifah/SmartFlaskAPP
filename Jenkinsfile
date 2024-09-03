pipeline {
    agent any
	environment {
        registry = "jehaddocker82/my-smart-app"
        img = "$registry"+":${env.BUILD_ID}"
        registryCredential = "dockerhub-login"
    }	

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/jehadkalifah/SmartFlaskAPP.git'
                sh 'ls -la'
            }
        }
        stage('Build') {
            steps {
				echo "Building our image"
				script {
                    // the whole command to build the image
					dockerImg = docker.build("${img}")
                }
            }
        }
        stage('Push') {
            steps {
				echo "Pushing our image"
				script {
                    // docker.withRegistry('https://registry.hub.docker.com', registryCredential)
                    withDockerRegistry(credentialsId: 'dockerhub-login') {
                        dockerImg.push()
                        // then the second one, it will be tagged as the latest
                        // so it will update the latest with the last image is pushed
                        dockerImg.push('latest')
                    }
                }
            }
        }        
    }
}
