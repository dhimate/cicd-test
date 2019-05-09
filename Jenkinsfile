pipeline {
    agent any
    /* {
        docker {
            image 'maven:3.6.1-jdk-8-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }*/
    
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
                configFileProvider([configFile(fileId: 'my_settings', variable: 'SETTINGS')]) {
                    sh "'mvn' -s $SETTINGS -Dmaven.test.failure.ignore clean package"
                }
            }
        }
   
       stage('Deploy') {
          // Deploy the maven build
            steps {
                configFileProvider([configFile(fileId: 'my_settings', variable: 'SETTINGS')]) {
                    sh "'mvn' -s $SETTINGS deploy -DmuleDeploy -Dtarget=${TARGET} -Dtarget.type=${TARGET_TYPE} -Dusername=${USERNAME} -Dpassword=${PASSWORD} -Denvironment=${ENVIRONMENT} "
                }
            }
        }
    } 
}