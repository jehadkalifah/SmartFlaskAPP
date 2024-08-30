pipeline {
    agent any
	environment {
        // define an image tag name
        def img = ("${env.JOB_NAME}:${env.BUILD_ID}").toLowerCase()
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
        stage('Deploy Run') {
            steps {
				echo "Deploy and Run"
				script {
                    // run the docker image and add the container id in count variable
					cont = docker.image("${img}").run('--rm -d -p 5000:5000')
					sleep(5)
                }
            }
        }
        stage('Do Some Tests') {
            steps {
				echo "Do Some tests"
            }
        }
    }
   post {
		 always  {
            echo "In POST stage - Stop Docker image"
            script {
                if (cont) {
                    echo "In Post - inside if condt"
                    // stop the container
                    cont.stop()
                }
            }
        }
	}
}
