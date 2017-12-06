#!groovy


try {


   node ('aws') {
        
        stage('Deployment on DEV') {
            checkout scm

          
            sh 'docker-compose -f local-compose.yml build apache'
            sh 'docker-compose -f local-compose.yml up -d apache'
            sh 'sleep 10'
	    sh 'docker images -a -q'
            sh 'docker tag bitnami/apache  localhost:5000/apache:latest'
            sh 'docker push localhost:5000/apache:latest'
           }  
        
    }

}




}
