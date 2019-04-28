properties([pipelineTriggers([githubPush()])]) 
node('linux'){
    stage('Unit Tests'){
      sh "ant -f test.xml -v"
      junit 'reports/result.xml'
    }
    stage('Build'){
        git 'https://github.com/kemioye/java-project.git'
        sh "ant"
        sh "ant -f build.xml -v"
    }
}
