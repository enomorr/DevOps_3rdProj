pipeline{
    agent any
    stages{
        stage ("First test pipeline" ){
         steps {
          echo "Hello There!!!"   
         }   
        }
        stage ("pulling github code"){
            steps {
               git branch: 'main', url: 'https://github.com/enomorr/DevOps_3rdProj.git' 
            }
        }
        stage ("Docker build stage"){
            steps {
                sh 'docker image build -t $JOB_NAME:v$BUILD_NUMBER .' 
                sh 'docker image tag $JOB_NAME:v$BUILD_NUMBER moreno1/$JOB_NAME:v$BUILD_NUMBER'
                sh 'docker image tag $JOB_NAME:v$BUILD_NUMBER moreno1/$JOB_NAME:latest'
            }
        }
        stage ("pushing docker image to dockerhub"){
            steps {
                sh 'docker push moreno1/$JOB_NAME:latest'
            }
        }
        stage ("building a container from image"){
            steps {
                sh'docker container stop enomordevops'
                sh 'docker container rm enomordevops'
                sh 'docker run --name enomordevops --hostname enomortest1 -p 8000:80 moreno1/test1:latest'
            }
        }
    
    }
}
 
