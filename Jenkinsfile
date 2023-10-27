pipeline {
    agent any
    environment {
        DOCKER_REGISTRY_URL = 'https://7tiuxysa.c1.gra9.container-registry.ovh.net'
        DOCKER_PROJECT_NAME = 'mydemoproject'
    }
 
    stages {
        stage('Build and Push React Image') {
            steps {
                dir('react') {
                    script {
                        echo "DOCKER_REGISTRY_URL: ${DOCKER_REGISTRY_URL}"
                        def harborImage = "${DOCKER_PROJECT_NAME}/harborimg:${env.BUILD_ID}"
                        docker.build(harborImage, "-f dockerfile .")
                        docker.withRegistry('https://7tiuxysa.c1.gra9.container-registry.ovh.net', 'ovh-registry-credentials') {
                            docker.image(harborImage).push()
                        }
                    }
                }
            }
        }
    }
}        