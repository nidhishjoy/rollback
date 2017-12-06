#!groovy


try {


   node ('aws') {
        
        stage('Deployment on DEV') {
            checkout scm

          
            sh 'docker-compose -f local-compose.yml build nginx-proxy'
            sh 'docker-compose -f local-compose.yml up -d nginx-proxy'
            sh 'sleep 10'
            sh 'docker tag nginx-proxy  localhost:5000/nginx-proxy:latest'
            sh 'docker push localhost:5000/nginx-proxy:latest'
           }  
        
    }

}



 catch (err) {
    currentBuild.result = "FAILED"
        mail (to: 'buzztime-players@hashedin.com',
             subject: "Job '${env.JOB_NAME}'- (${env.BUILD_NUMBER}) has FAILED",
             body: "Please go to ${env.BUILD_URL} for more details. ");

        throw err
  }


finally {
  node ('aws')
 sh 'docker ps'

}
