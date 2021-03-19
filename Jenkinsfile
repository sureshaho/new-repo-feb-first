node{
  stage('SCM checkout'){
     git 'https://github.com/sureshaho/new-repo-feb-first'
  }
  stage('Build'){
     sh 'mvn package'
  }
}
