node {
  
  stage('Checkout Source Code') {
    checkout scm
  }

  stage('Create Docker Image') {
    docker.build("docker_image:${env.BUILD_NUMBER}")
  }

  stage ('Run Application') {
    try {
      // Stop existing Container
      sh 'docker rm docker_container -f'
      // Start database container here
      sh "docker run -d --name docker_container docker_image:${env.BUILD_NUMBER}"
    } 
	catch (error) {
    } finally {
      // Stop and remove database container here
      
    }
  }
  
  stage ('Notifications') {
    mail body: "Project Execution Completed with status : " + currentBuild.result ,
                     subject: 'Simplilearn Project1 for Dockerizing Jenkins Pipeline',
                     to: 'john.levin@globallogic.com'
     }
 }
