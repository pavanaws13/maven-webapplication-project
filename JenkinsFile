node
{

   def mavenHome= tool name: "maven-3.9.16"
   stage('git checkout')
   {
      git branch: 'master', url: 'https://github.com/pavanaws13/maven-webapplication-project.git'
   }
   stage('COMPILE')
   {
    sh  "${mavenHome}/bin/mvn compile" 
   }
   stage('SQ REPORT')
   {
        sh  "${mavenHome}/bin/mvn sonar:sonar" 
   }
   stage('Build')
   {
     sh  "${mavenHome}/bin/mvn package"
   }
   stage('Deploy to Nexus')
   {
      sh  "${mavenHome}/bin/mvn deploy"
   }

   stage('Deploy to Tomcat') 
    {
      
      sh """

      curl -u admin:P@vanr13 \
--upload-file /var/lib/jenkins/workspace/Maven-Scripted-Way-PL/target/maven-web-application.war \
"http://15.207.110.77:8080/manager/text/deploy?path=/maven-web-application&update=true"
          
        """
    }
	
} //node ending
