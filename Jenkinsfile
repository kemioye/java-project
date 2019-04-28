node('linux'){
    stage('Build'){
        git 'https://github.com/kemioye/java-project.git'
        sh "ant"
        sh "ant -f build.xml -v"
    }
}
