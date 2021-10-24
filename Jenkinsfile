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
stage("Quality Gate"){
  timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
    def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
    if (qg.status != 'OK') {
      error "Pipeline aborted due to quality gate failure: ${qg.status}"
    }
  }
}
