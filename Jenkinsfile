node {
	def application = "myproject"
	def dockerimagename = "myprojectimg"
	def dockerhubaccountid = "krupadevi"
	stage('Clone repository') {
		checkout scm
	}

	stage('Build image') {
		app = docker.build("${dockerimagename}:${BUILD_NUMBER}")
	}
        stage('Push image') {
		withDockerRegistry([ credentialsId: "dockerhubaccountid", url: "" ]) {
		app.push()
		app.push("latest")
	}
	stage('Deploy') {
		sh ("docker run -d -p 81:8080 -v /var/log/:/var/log/ ${dockerimagename}:${BUILD_NUMBER}")
	}
	
	stage('Remove old images') {
		// remove docker pld images
		sh("docker rmi ${dockerimagename}:latest -f")
   }
}
}
