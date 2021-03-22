properties([parameters([choice(choices: 'master\ndev\nQA', description: 'Please Pick branch to build', name: 'branch')])])

def getVersion(){
	def commithash = sh returnStdout: true, script: 'git rev-parse   --short HEAD' 
	return commithash
}

environment {
  DOCKER_TAG = "getVersion()"
}

node{
  stage('SCM checkout as per User'){
     echo "pull code from git at run time ${params.branch}"
     git url: 'https://github.com/sureshaho/new-repo-feb-first', branch: "${params.branch}"
  }
  stage('Build'){
     def mvnhome = tool name: 'Maven', type: 'maven'
     sh "${mvnhome}/bin/mvn package"
  }
  stage('Tomcat Deployment'){
     sshagent(['tomcat-dev']) {
     sh 'scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/jenkin-git-and-maven/webapp/target/*.war  ec2-user@172.31.13.162:/opt/tomcat/apache-tomcat-8.5.64/webapps'
  }
  }
  stage('Build the docker image'){
     sh 'cp /var/lib/jenkins/workspace/jenkin-git-and-maven/webapp/target/webapp.war /var/lib/jenkins/workspace/jenkin-git-and-maven'
     sh 'docker build . -t sureshaho/simple-dev-op-image-latest:0.0.12'
  }
  stage('Push the docker image to Docker Hub'){
     withCredentials([string(credentialsId: 'docker-hub', variable: 'docker-hub-variable')]) {
      sh 'docker login -u sureshaho -p ${docker-hub-variable}' 
     }
     sh 'docker push sureshaho/simple-dev-op-image-latest:0.0.12'
    
  }
}
