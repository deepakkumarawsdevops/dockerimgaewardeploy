pipeline {
    agent  { label 'docker_node_build'}

    environment
    {
     DOCKERHUB_CREDENTIALS = credentials('docker-hub-login')

    }


    stages {

          stage('Java Build')
	  {
	  
          steps
	  {
            echo 'Building'
	    sh 'mvn package'
	    sh 'mvn install'
	  } 

	  }
           stage('BuildDockerImage') {
            steps {
                echo 'Imageing..'
                 sh 'docker build -t deepakkumarawsdevops/warapp:$BUILD_NUMBER .'
                                                        
 
            }  
        }

        stage('LogintoDockerHub')

        {
         steps{
           sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                                                               
         }



        }
        stage('ReleaseToDockerHub'){

          steps {
             echo 'Releasing...'
              sh 'docker push deepakkumarawsdevops/warapp:$BUILD_NUMBER'

              }

            }
         stage('Deployment') {
	 agent { label 'docker_node_build1'}
            steps {
                echo 'Deploying....'

              sh 'docker container run -dt --name localapp -p 8085:8080 deepakkumarawsdevops/warapp:$BUILD_NUMBER'
            }
        }

    }

    }

