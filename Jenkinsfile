node {
    stage('Git Checkout'){
      git 'https://github.com/anand1192/JenkinsHtml.git'
    }
      stage('Pre-Build Stage'){
          sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 786678469955.dkr.ecr.ap-south-1.amazonaws.com'
      }
      stage('Build Stage'){
          def REPOSITORY_URI = '786678469955.dkr.ecr.ap-south-1.amazonaws.com/jenkinsrepo'
          sh "docker build -t jenkinsrepo ."
          sh "docker tag jenkinsrepo:latest 786678469955.dkr.ecr.ap-south-1.amazonaws.com/jenkinsrepo:latest"
      }
      stage('Deploy Docker Image'){
          def REPOSITORY_URI = '786678469955.dkr.ecr.ap-south-1.amazonaws.com/jenkinsrepo'
          sh "docker push 786678469955.dkr.ecr.ap-south-1.amazonaws.com/jenkinsrepo:latest"
      }
 }
