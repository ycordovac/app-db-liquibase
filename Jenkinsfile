pipeline {
  agent {
    docker { image 'liquibase/liquibase:4.15.0' }
  }
  environment {
    POSTGRES_CREDENTIALS=credentials('postgres-credentials')
  }
  stages {
    stage('Status') {
      steps {
        sh 'liquibase status --url="jdbc:postgresql://192.168.49.7:5432/postgres?currentSchema=public" --changeLogFile=app-wrapper.xml --username=$POSTGRES_CREDENTIALS_USR --password=$POSTGRES_CREDENTIALS_PSW'
      }
    }
    stage('Update') {
      steps {
        sh 'liquibase update --url="jdbc:postgresql://192.168.49.7:5432/postgres?currentSchema=public" --changeLogFile=app-wrapper.xml --username=$POSTGRES_CREDENTIALS_USR --password=$POSTGRES_CREDENTIALS_PSW'
      }
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}