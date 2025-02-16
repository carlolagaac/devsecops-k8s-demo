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
    }
}