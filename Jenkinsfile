node{
    
    stage('git checkout'){
        git credentialsId: 'git-creds', url: 'https://github.com/shubhamkushwah123/war-test.git'
    }
    
    stage('build & test'){
        //sh 'mvn clean package'
        def mavenHome = tool name: 'maven-3', type:'maven'
        def mavenCMD = "${mavenHome}/bin/mvn"
        sh "${mavenCMD} clean package"
        
    }
    
    stage('deploy to tomcat'){
        deploy adapters: [tomcat8(credentialsId: 'tomcat-creds-final', path: '', url: 'http://localhost:8888')], contextPath: 'bootcamp4', war: '**/*.war'
    }
    
    stage('build docker image'){
        sh 'docker build -t pripatil/bootcamp3:1.0.2'
        }
    
    stage('push docker image to docker hub'){
      sh 'docker push pripatil/bootcamp3:1.0.2'
      }
    
    stage('run the docker image'){
    sh 'docker run -p 8888:8080 pripatil/bootcamp3:1.0.2'
    }
    
    //stage('run the docker image on cloud'){
    //sh 'ssh -i aws-key ec2-user@publickey'
    //sh 'docker run -p 8888:8080 pripatil/bootcamp3:1.0.2'
    //}   
}