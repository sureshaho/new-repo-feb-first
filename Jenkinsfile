properties([parameters([choice(choices: 'master\ndev\nQA', description: 'Please Pick branch to build', name: 'branch')])])

node{
  stage('SCM checkout as per User'){
     echo "pull code from git at run time ${params.branch}"
     git url: 'https://github.com/sureshaho/new-repo-feb-first', branch: "${params.branch}"
  }
  stage('Build'){
     def mvnhome = tool name: 'Maven', type: 'maven'
     sh "${mvnhome}/bin/mvn package"
  }
  stage('Email notification'){
   mail bcc: '', body: 'Hello how are you Gayathri', cc: '', from: '', replyTo: '', subject: 'Notofications', to: 'suresha.ho@gmail.com'
  }
}
