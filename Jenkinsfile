node{
  stage('SCM checkout'){
     
     git 'https://github.com/sureshaho/new-repo-feb-first'
  }
  stage('Build'){
     def mvnhome = tool name: 'Maven', type: 'maven'
     sh "${mvnhome}/bin/mvn package"
  }
}
