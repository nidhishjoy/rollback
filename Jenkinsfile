#!groovy


try {


   node ('aws') {
        
        stage('Deployment on DEV') {
            checkout scm

          
            sh 'docker-compose -f local-compose.yml build apache'
            sh 'echo "start"'
            sh 'docker-compose -f local-compose.yml up -d apache'
	    sh 'echo "stop"'
            sh 'sleep 10'
	    sh 'docker images -a -q'
            sh 'docker tag bitnami/apache  localhost:5000/apache:$BUILD_NUMBER'
            sh 'docker push localhost:5000/apache:$BUILD_NUMBER'
           }  
        
    }

	node ('master') {
          stage('creating parameter for jenkins') {      
           sh 'touch /home/build/$BUILD_NUMBER'
	 
     }
  }

}



finally {

    node ('aws') {
        stage('Cleanup on testing host') {
            sh 'docker ps'
         }
   }
}
