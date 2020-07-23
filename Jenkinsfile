node {
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("itexperts0247/testdocker:nodejs")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }

    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'GitHub') {
	       app.push("${env.BUILD_NUMBER}")
 	       app.push("latest")
            } 
                echo "Trying to Push Docker Build to DockerHub"
	    
	    //stage('Run Container on Dev Server'){
    		//def dockerRun = 'sudo docker run -ti -d -p 8000:8000 itexperts0247/testdocker'
     		//sshagent(['dev-server']) {
       		//sh "ssh -o StrictHostKeyChecking=no devops@193.70.111.126 ${dockerRun}"
     //}
   //}
  }
}
