node{
  stage('SCM checkout'){
     
     git 'https://github.com/sureshaho/new-repo-feb-first'
  }
  stage('Build'){
     def mvnhome = tool name: 'Maven', type: 'maven'
     sh "${mvnhome}/bin/mvn package"
  }
  stage('Email notification'){
   mail bcc: '', body: 'Hello how are you Vinayak', cc: '', from: '', replyTo: '', subject: 'Notofications', to: 'suresha.ho@gmail.com'
  }
}
