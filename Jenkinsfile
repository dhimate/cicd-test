pipeline {
    agent 
    {
        docker {
            image 'maven:3.6.1-jdk-8-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    
    stages {
        stage('Preparation') { // for display purposes
        // Get some code from a GitHub repository
            steps {
              //git 'https://github.com/dhimate/gateway-proxy-domain.git'
        	      //sh "'mvn' -Dmaven.test.failure.ignore clean package install"
              git (
                  url: 'https://github.com/dhimate/cicd-test.git',
                  credentialsId: 'github_id'
                  )
              sh 'git config credential.helper store'
              sh 'git clean -f'
              sh 'git checkout .'
            }
        }
 /*       stage('Build') {
          // Run the maven build
            steps {
                configFileProvider([configFile(fileId: 'my_settings', variable: 'SETTINGS')]) {
                    sh "'mvn' -s $SETTINGS -Dmaven.test.failure.ignore clean package"
                }
            }
        }
*/  
       stage('Deploy') {
          // Deploy the maven build
            steps {
                configFileProvider([configFile(fileId: 'my_settings', variable: 'SETTINGS')]) {
                    sh "'mvn' -s $SETTINGS clean package deploy -DmuleDeploy -Dtarget=${TARGET} -Dtarget.type=${TARGET_TYPE} -Dusername=${USERNAME} -Dpassword=${PASSWORD} -Denvironment=${ENVIRONMENT} "
                }
            }
        }
        
        stage('Results') {
            steps {
                junit '**/target/surefire-reports/TEST-*.xml'
                //archiveArtifacts 'target/*.jar'
            }
        }
    } 
}