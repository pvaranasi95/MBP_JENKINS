pipeline {
    agent any
    tools {
        jdk 'JDK11'  //JDK17
        maven 'Maven'
    }

    stages {
        stage('Is UNIX') {
            steps {
                isUnix()
            }
        }
        stage ('Git Clone') {
            steps{
                git clone -b %JOB_NAME% https://github.com/pvaranasi95/MBP_JENKINS.git
            }
        }
        stage('Sonar scan') {
            steps{
                script{
                bat 'cd C:\Users\pavan\OneDrive\Desktop\DevOps\sonarqube-10.4.1.88267\bin\windows-x86-64'
               bat 'sonar-scanner.bat -D"sonar.projectKey=MBP_JENKINS" -D"sonar.sources=." -D"sonar.host.url=http://localhost:9000" -D"sonar.token=sqp_e74e2517f3622c5da7fe884b1db3d96cc76bb3d5"'
                 }
            }
        }
         stage('Change Directory') {
             steps{
                bat 'cd C:\\Users\\pavan\\OneDrive\\Desktop\\DevOps\\Python'
             }
         }
         stage('Docker Image') {
             steps{
                 bat 'docker build -t pvaranasi/py-num-guess:%BUILD_NUMBER% .'
             }
         }
         stage('Docker Push') {
             steps{
                 bat 'docker push pvaranasi/py-num-guess:%BUILD_NUMBER%'
             }
         }
         stage('Container') {
             steps{
                 bat 'docker run -d -p 8088:80 --name py-num-guess:%BUILD_NUMBER% py-num-guess:%BUILD_NUMBER%'
             }
         }
     }
    post{
        failure{
            emailext subject: "Build Failed for:%JOB_NAME% with %BUILD_NUMBER%",
                body: "Hi Your jenkins Build is failed for %JOB_NAME% with %BUILD_NUMBER%",
                to: "pavanvaranasi95@gmail.com",
                from: "pavanvaranasi95@gmail.com"
        }
        success{
            emailext subject: "Build success for %JOB_NAME% with %BUILD_NUMBER%",
                body: "Hi Your jenkins Build is success for %JOB_NAME% with %BUILD_NUMBER%",
                to: "pavanvaranasi95@gmail.com",
                from: "pavanvaranasi95@gmail.com"
        }
    }
}
