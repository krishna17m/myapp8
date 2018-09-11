try{
node{
   stage('Git Clone'){
        git 'https://github.com/krishna17m/myapp8'
    }
    stage('Maven Build'){
        sh 'mvn clean package'
    }
    stage('Deploy to Tomcat'){
        sh 'mv target/*.war target/test.war'

           sh 'sudo rm -rf /root/tomcat8/apache-tomcat-8.5.33/webapps/test*.war'
            sh 'sudo cp target/test.war /root/tomcat8/apache-tomcat-8.5.33/webapps/'
            sh 'service tomcat stop'
            sh 'service tomcat start'
        slackSend color: 'good',
        message: "Job ${env.JOB_NAME} deployed Successfully having build ${env.BUILD_URL}"
   }

}
}
catch(error){
   slackSend color: 'danger',
        message: "Job ${env.JOB_NAME} deployment failed having build ${env.BUILD_URL}"
        error''
}
