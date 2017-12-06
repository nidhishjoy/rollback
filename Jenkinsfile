#!groovy


try {


   node ('aws') {
        docker.withRegistry('localhost:5000') {
        stage('Deployment on DEV') {
            checkout scm

          
            sh 'docker-compose -f local-compose.yml build node'
            sh 'docker-compose -f local-compose.yml up -d node'
            sh 'sleep 10'
            sh 'docker tag nginx-proxy  localhost:5000/nginx:latest
            sh 'docker push localhost:5000/nginx:latest
           }  
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

    node ('aws') {
        stage('Cleanup on deployment host') {
            sh 'docker ps --no-trunc --all --quiet --filter="status=exited" | xargs --no-run-if-empty docker rm || true'
            sh 'docker images --no-trunc --all --quiet --filter="dangling=true" | xargs --no-run-if-empty docker rmi || true'
            sh 'docke ps'
         }
   }
}

