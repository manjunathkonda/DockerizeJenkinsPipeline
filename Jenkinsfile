node {
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'manjunathkonda/dockerize-jenkins'
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
		 script {
         newApp = docker.build registry + ":$BUILD_NUMBER"
		 }
        
	}
	stage('Deploying image') {
		script {
          docker.withRegistry( '', registryCredential ) {
            newApp.push()
          }
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
