pipeline {
  agent any
  stages {
    stage('Build Backend') {
      steps {
        echo 'Building backend'
        sh 'cd backend && ./mvnw package'
      }
    }
    stage('Building Frontend') {
      steps {
        echo 'Building frontend'
        sh 'cd frontend && npm install && ng build'
      }
    }
    stage('Archive Artifacts') {
      steps {
        archiveArtifacts 'backend/target/*.jar'
        archiveArtifacts './frontend/dist/*'
      }
    }
  }
}