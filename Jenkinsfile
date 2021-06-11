node{
   stage('SCM Checkout'){
       git crediantialsId: 'git-creds', url: 'https://github.com/javahometech/my-app'
    }
    stage('Mvn Package'){
        def mvnHome = tool name: 'maven-3, type: 'maven'
        def mvnCMD = "${mvnHome}/bin/mvn"
        sh "${mvnCMD} clean package"
    } 
    stage('Build Docker Image'){
        sh 'docker build -t 992652/my-app:2.0.0 .'
    }
    stage('Push Docker Image'){
        withCredentials([string(crediantialsId: 'docker-pwd', variable: 'dockerHubPwd')]) {
            sh "docker login -u 992652 -p $(dockerHubPwd)"
        }
        sh 'docker push 992652/my-app:2.0.0'
    }
    stage('Run Container on Dev Server'){
        def 'docker run -p 8080:8080 -d --name my-app 992652/my-app:2.0.0'
        sshagent(['dev-server']){
            sh "ssh -o StrictHostKeyChecking=no ec2-user@
    }
    
    }
}