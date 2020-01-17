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
        docker.withRegistry( 'https://hub.docker.com/repository/docker/' + registry, registryCredential ) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}
	stage('Registring image') {
        docker.withRegistry( 'https://hub.docker.com/repository/docker/' + registry, registryCredential ) {
    		newApp.push 'latest2'
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
