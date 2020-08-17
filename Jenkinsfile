node {

    checkout scm

    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {

        def customImage = docker.build("ak217/dockerpythonserver")

        /* Push the container to the custom Registry */
        customImage.push()
    }
}
