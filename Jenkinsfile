pipeline {
    agent  { label 'docker_node_build'}

    environment
    {
     DOCKERHUB_CREDENTIALS = credentials('docker-hub-login')

    }


    stages {


           stage('BuildDockerImage') {
            steps {
                echo 'Imageing..'
                sh 'docker build -t deepakkumarawsdevops/newappwar:$BUILD_NUMBER .'


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
              sh 'docker push deepakkumarawsdevops/newappwar:$BUILD_NUMBER'

              }

            }
         stage('Deployment') {
	 agnet { label 'docker_node_build1'}
            steps {
                echo 'Deploying....'

              sh 'docker container run -dt --name appwar -p 8084:8080 deepakkumarawsdevops/newappwar:$BUILD_NUMBER'
            }
        }

    }

    }

