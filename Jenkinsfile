#!groovy


try {


   node ('aws') {
        
        stage('Deployment on DEV') {
            checkout scm

          
            sh 'docker-compose -f local-compose.yml build node'
            sh 'docker-compose -f local-compose.yml up -d node'
            sh 'sleep 10'
            sh 'docker tag nginx-proxy  localhost:5000/nginx:latest'
            sh 'docker push localhost:5000/nginx:latest
           }  
        
    }



}

