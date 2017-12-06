#!groovy


try {


   node ('aws') {
        
        stage('Deployment on DEV') {
            checkout scm

          
            sh 'docker-compose -f local-compose.yml build nginx'
            sh 'docker-compose -f local-compose.yml up -d nginx'
            sh 'sleep 10'
	    sh 'docker images -a -q'
            sh 'docker tag apache  localhost:5000/apache:latest'
            sh 'docker push localhost:5000/apache:latest'
           }  
        
    }

}



 catch (err) {
    currentBuild.result = "FAILED"
        mail (to: 'nidhish.joy@hashedin.com',
             subject: "Job '${env.JOB_NAME}'- (${env.BUILD_NUMBER}) has FAILED",
             body: "Please go to ${env.BUILD_URL} for more details. ");

        throw err
  }


finally {
  node ('aws')
 sh 'docker ps'

}
