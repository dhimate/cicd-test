node {
   def mvnHome = "/opt/maven"
   def jobName = env.JOB_NAME
   def projectName = jobName.split('/')[0]
   echo "Job Name ${jobName}"
   echo "Project Name ${projectName}"
   stage('Preparation') { 
      // Get code from a GitHub repository
      git 'https://github.com/dhimate/gateway-proxy-domain.git'
	  sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package install"
      git "https://github.com/dhimate/${projectName}.git"
           
   }
   stage('Build') {
      // Run the maven build
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore -DskipMunitTests clean package"
   }
   
   stage('Deploy') {
      // Run the maven build
      sh "'${mvnHome}/bin/mvn' deploy -DmuleDeploy -DskipMunitTests -Dtarget=${MULE_SANDBOX_TARGET} -Dtarget.type=${MULE_SANDBOX_TARGET_TYPE} -Dusername=${MULE_USERNAME} -Dpassword=${MULE_PASSWORD} -Denvironment=${MULE_SANDBOX_ENVIRONMENT}"
   }
   
}
