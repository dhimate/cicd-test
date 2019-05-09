pipeline {
    agent {
        any {
        }
    }
    
    stages {
        stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
            steps {
              git 'https://github.com/dhimate/gateway-proxy-domain.git'
        	  sh "'mvn' -Dmaven.test.failure.ignore clean package install"
              git 'https://github.com/dhimate/cicd-test.git'
            }
        }
        stage('Build') {
          // Run the maven build
            steps {
                sh "'mvn' -Dmaven.test.failure.ignore clean package"
            }
        }
   
       stage('Deploy') {
          // Deploy the maven build
            steps {
                sh "'mvn' deploy -DmuleDeploy -Dtarget=${MULE_SANDBOX_TARGET} -Dtarget.type=${MULE_SANDBOX_TARGET_TYPE} -Dusername=${MULE_USERNAME} -Dpassword=${MULE_PASSWORD} -Denvironment=${MULE_SANDBOX_ENVIRONMENT} "
            }
        }
    } 
}

