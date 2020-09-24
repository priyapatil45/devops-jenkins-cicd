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
    
}