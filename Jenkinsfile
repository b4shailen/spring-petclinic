pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.projectKey=PetClinic \\
  -Dsonar.projectName=\'PetClinic\' \\
  -Dsonar.host.url=http://172.31.16.170:9000 \\
  -Dsonar.token=sqp_32b944f85238478ea9da7053d60d8223277b1249'''
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
        junit(testResults: '**/target/surefire-reports/*.xml', allowEmptyResults: true)
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
      }
    }

  }
}