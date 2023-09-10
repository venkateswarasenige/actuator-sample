node{
    stage ('scm checkout'){
        git credentialsId: 'git-credential', url: 'https://gitlab.com/venkateswar/actuator-sample.git'
    }
    stage ('mvn package'){
        def mvnHome=tool name: 'maven-3', type: 'maven'
        def mvnCMD= "${mvnHome}/bin/mvn"
        sh "${mvnCMD} clean package"
    }
    stage ('build docker image'){
        withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerHub pwd')]) {
        sh 'docker login -u svdevops -p ${dockerHub pwd}'
    }
    
        sh 'docker build -t svdevops/sbtr-repo:2.0.0 .'
}