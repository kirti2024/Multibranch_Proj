
pipeline{
	agent any
	environment{
	DOCKER_PASSWORD="dtoken"
		
}
		stages{
			stage('Checkout'){
				steps{
					script{
   checkout scmGit(branches: [[name: '*/milbr1']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kirti2024/Multibranch_Proj.git']])
}
				}
			}
			stage('build image'){
				steps{
					script{
						sh 'docker buildx build -t assesimage22:16 .'
						
						sh 'docker tag assesimage22:16 kirti2024/assessmentpurpose:115'
						
																
}
}
}
	stage ('push image'){
		steps{
			 script{
				 withCredentials([usernamePassword(credentialsId: "${DOCKER_PASSWORD}", usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh """
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker push kirti2024/assessmentpurpose:115
                        """
            }

 
			 }
			}
}



stage('Deploy to K8s'){
              steps{
		script{ 
	
		withKubeConfig(caCertificate: '', clusterName: 'mbranch-cluster', contextName: '', credentialsId: 'eksclustertoken', namespace: '', restrictKubeConfigAccess: false, serverUrl: 'https://DABA616145FB345829A8EA58861FAD41.gr7.us-east-1.eks.amazonaws.com') {
    			sh """ helm create nginx-chart """
			
			//sh """ kubectl apply -f jenkins.yaml """
}

			}
		}
	      }

			
}
}
