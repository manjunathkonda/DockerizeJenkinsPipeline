node {
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'manjunathkonda/dockerrize-jenkins'
    def registryCredential = 'dockerhub'
	
	stage('Git') {
		git 'https://github.com/manjunathkonda/DockerizeJenkinsPipeline.git'
	}
	stage('Build') {
		sh 'npm install'
		
	}
	stage('Test') {
		
	}
	stage('Building image') {
         newApp = docker.build registry + ":$BUILD_NUMBER"
        }
	}
	stage('Registring image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
    		newApp.push 'latest2'
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
