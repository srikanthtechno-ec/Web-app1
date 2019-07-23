node{
    
    //def mvnHome = tool name: 'maven 3.6.1', type: 'maven'
    def mvnHome = tool name: 'maven 3.6.1', type: 'maven'
    properties([buildDiscarder(logRotator(numToKeepStr: '3'))])
    
     
    stage('Checkout'){
        git credentialsId: '22d801d0-a4ec-4bc0-b7ef-d4e6dd550d84', url: 'https://github.com/srikanthtechno-ec/Web-app1.git'
    }
    
    stage('Build'){
        sh "${mvnHome}/bin/mvn clean package"
    }
    
    stage('SonarQube'){
        sh "${mvnHome}/bin/mvn sonar:sonar"
    }
    
    stage('Nexus upload'){
        sh "${mvnHome}/bin/mvn deploy"
    }
    
    stage('Deployapptotomcat'){
        
       // sshagent(['tomcat-server']) {
    // some block
    //sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@13.233.70.9:/opt/tomcat/webapps/"
      //  }
        //sshagent(['tomcat-server']) {
        //sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@13.233.123.253:/opt/tomcat/webapps/"
        //}
        sshagent(['tom']) {
    // some block
    sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@13.233.70.9:/opt/apache-tomcat-9.0.21/webapps/"
}
    }
    
    stage('Sendemail'){
        mail bcc: '', body: '''Hai 

i am from jenkins

Regards,
Pipeline''', cc: '', from: '', replyTo: '', subject: 'Jenkins mail', to: 'srikanth.shukrith@gmail.com'
        
    }
    
    
    
}
