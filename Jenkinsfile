
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
						sh 'docker buildx build -t mbranchimage2:15 .'
						
						sh 'docker tag mbranchimage2:15 kirti2024/mbranchpurpose:15'
						
																
}
}
}
	stage ('push image'){
		steps{
			 script{
				 withCredentials([usernamePassword(credentialsId: "${DOCKER_PASSWORD}", usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh """
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                        docker push kirti2024/mbranchpurpose:15
                        """
            }

 
			 }
			}
}



stage('Deploy to K8s'){
              steps{
		script{ 
			withKubeConfig(caCertificate: '', clusterName: 'mbranch-cluster', contextName: '', credentialsId: 'eksclustertoken', namespace: '', restrictKubeConfigAccess: false, serverUrl: 'https://DABA616145FB345829A8EA58861FAD41.gr7.us-east-1.eks.amazonaws.com') {
    sh """ kubectl apply -f jenkins.yaml """
}

			}
		}
	      }

			
}
}
