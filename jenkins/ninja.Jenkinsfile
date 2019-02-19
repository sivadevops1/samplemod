
pipeline {
  agent any
  stages {
    //Stage for Code checkout from git  
    stage('CodeCheckout') {
      steps {
	    script {
		  checkout scm
		}
      }
   	} /* code checkout ends */
	
	/*This will get a Python image and build the new docker image */
	stage('Python Build') {
      steps {
	    script {
		  checkout scm
		}
      }
   	} /* Python Build ends */
  	
	stage('Docker Integration to Hub') {
      steps {
	    script {
		  sh 'docker build -t rakeshraheja89/project .'
		  sh "docker login --username=$env.username --password=$env.password"
		  sh 'docker push rakeshraheja89/project'
		}
      }
   	} /* Python Build ends */
	
	stage('Deploy to K8') {
      steps {
	  kubernetesDeploy (
        kubeconfigId: 'kubeconfig',
        configs: 'application.yaml',
        enableConfigSubstitution: false
        )
      }
    } /* Kubernetes ends */
 
    }//stages ends here
}//pipeline ends here
