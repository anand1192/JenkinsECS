node {
    stage('Git Checkout'){
      git 'https://github.com/anand1192/JenkinsHtml.git'
    }
      stage('Pre-Build Stage'){
          sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 786678469955.dkr.ecr.ap-south-1.amazonaws.com'
          sh "COMMIT_HASH=$(echo $CODEBUILD_RESOLVED_SOURCE_VERSION | cut -c 1-7)"
          sh "IMAGE_TAG=build-$(echo $CODEBUILD_BUILD_ID | awk -F":" '{print $2}')"
      }
      stage('Build Stage'){
          sh 'docker build -t $REPOSITORY_URI:latest .'
          sh 'docker tag $REPOSITORY_URI:latest $REPOSITORY_URI:$IMAGE_TAG'
      }
      stage('Deploy Docker Image'){
              sh "docker push $REPOSITORY_URI:latest"
              sh 'docker push $REPOSITORY_URI:$IMAGE_TAG'
      }
 }
