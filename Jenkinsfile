pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'release',
                    url: 'https://github.com/pvaranasi95/MBP_JENKINS.git',
                    credentialsId: 'GitHub'
            }
        }

        stage('Is UNIX') {
            steps {
                isUnix()
            }
        }

        // Add other stages here as needed
    }

    post {
        failure {
            emailext subject: "Build Failed for: ${env.JOB_NAME} with ${env.BUILD_NUMBER}",
                body: "Hi, your Jenkins build has failed for ${env.JOB_NAME} with build number ${env.BUILD_NUMBER}.",
                to: "pavanvaranasi95@gmail.com",
                from: "pavanvaranasi95@gmail.com"
        }
        success {
            emailext subject: "Build Succeeded for: ${env.JOB_NAME} with ${env.BUILD_NUMBER}",
                body: "Hi, your Jenkins build was successful for ${env.JOB_NAME} with build number ${env.BUILD_NUMBER}.",
                to: "pavanvaranasi95@gmail.com",
                from: "pavanvaranasi95@gmail.com"
        }
    }
}
