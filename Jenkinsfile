pipeline {
  agent any

  options {
    timeout(time: 2, unit: 'MINUTES')
  }

  environment {
    ARTIFACT_ID = "elbuo8/webapp:${env.BUILD_NUMBER}"
  }
   stages {
   stage('Building image') {
      steps{
          sh '''
          #cd webapp
          docker build -t testapp .
             '''  
        }
    }
  
  
    stage('Run tests') {
      steps {
        sh "docker run testapp npm test"
      }
    }
   stage('Deploy Image') {
      steps{
        sh '''
        docker login -u admin -p admin 127.0.0.1:8082
        docker tag testapp 127.0.0.1:8082/misa/testapp
        docker push 127.0.0.1:8082/misa/testapp   
        '''
        }
      }
    }
}


    
  

