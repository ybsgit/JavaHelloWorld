node{
  stage('SCM checkout'){
    git 'https://github.com/ybsgit/JavaHelloWorld'
  }
  stage('compile and package')
  {
    sh 'mvn package'
  }
     stage('SonarQube Analysis') {
        withSonarQubeEnv('new-soanar') { 
          sh "mvn sonar:sonar"
        }
    }
}
