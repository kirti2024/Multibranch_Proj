
pipeline{
	agent any
	environment{
	DOCKER_PASSWORD="dtoken"
		
}
		stages{
			stage('Checkout'){
				steps{
					script{
   checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kirti2024/Multibranch_Proj.git']])
}
				}
			}
			stage('build image'){
				steps{
					script{
						sh 'docker buildx build -t mbranchngximage2:15 .'
						
						sh 'docker tag mbranchngximage2:15 kirti2024/mbranchngxpurpose:15'
						
																
}
}
}
	stage ('push image'){
		steps{
			 script{
				 withCredentials([usernamePassword(credentialsId: "${DOCKER_PASSWORD}", usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh """
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker push kirti2024/mbranchngxpurpose:15
                        """
            }

 
			 }
			}
}



stage('Deploy to K8s'){
              steps{
		script{ 
			sh """ helm install helmrelease ./nginx-helm """

			}
		}
	      }

			
}
}
