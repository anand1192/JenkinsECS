node{stage('Git Checkout'){
      git 'https://github.com/anand1192/JenkinsHtml.git'
    }
    stage('Build Docker Image'){
        sh 'docker build -t ak217/dockerpythonserver:2.0.0 .'
    }
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerpwd')]) {
            sh "docker login -u ak217 -p ${dockerpwd}"
        }
        sh 'docker push ak217/dockerpythonserver:2.0.0'
    }
    stage('Deploy Docker Image'){
        def RunCmd = 'docker run -p 8080:8080 -d --name HtmlWeb ak217/dockerpythonserver:2.0.0'
        sshagent(['dev-server']) {
            sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.46.149 ${RunCmd}"
        }
    }
}
