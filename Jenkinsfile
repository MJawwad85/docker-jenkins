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
	    stage('Run Container on Dev Server'){
    		def dockerRun = 'sudo docker run -p 8089:8089 -p 50000:50000 --name=jenkins-master --mount source=jenkins-log,target=/var/log/jenkins --mount source=jenkins-data,target=/var/jenkins_home -d jenkins-server itexperts0247/testdocker:nodejs-${BUILD_NUMBER}'
     		sshagent(['localhost']) {
       		sh "ssh -o StrictHostKeyChecking=no devops@193.70.111.126 ${dockerRun}"
     }
   }
    }
