pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //modified again #9
            }
        }  
        stage('Unit Test') {
            steps {
              sh "mvn test"
            }
            post {
              always {
                  publishHTML(
                      target: [
                          reportDir: 'target/site/jacoco',
                          reportFiles: 'index.html',
                          reportName: 'JaCoCo Coverage Report'
                      ]
                  )
              }
           }
        }  
        stage('Docker Build and Push') {
            steps {
              withDockerRegistry([credentialsId: "docker-hub", url: ""]){
                sh "printenv"
                sh 'docker build -t caizen/numeric-app:""$GIT_COMMIT"" .'
                sh 'docker push caizen/numeric-app:""$GIT_COMMIT""'
            }
        }

     }