pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Greenlight Example') {
		    steps {
		    //echo 'JDK:'
		    //bat 'java -version'
		      bat 'curl -O https://downloads.veracode.com/securityscan/gl-scanner-java-LATEST.zip'
		      bat 'unzip gl-scanner-java-LATEST.zip gl-scanner-java.jar'
		      bat '''java -jar gl-scanner-java.jar /
		        --api_id "${VERACODE_API_ID}" /
		        --api_secret_key "${VERACODE_API_SECRET}" /
		        --project_name "${env.JOB_NAME}" /
		        --project_url "${env.JOB_URL}" /
		        --project_ref "${env.GIT_COMMIT}"'''
		    }
		}
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
	post {
	    always {
	      archiveArtifacts artifacts: 'results.json', fingerprint: true
	    }
	}
}