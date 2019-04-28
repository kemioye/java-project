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
    stage('Deploy'){
        sh 'aws s3 cp /workspace/java-pipeline/dist/* s3://ustseis665-1-kemi'
    }
    stage('Reports'){
      withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS user for Jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
          sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
      }
    }
}
