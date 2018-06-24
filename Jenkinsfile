pipeline {
  agent any
  stages {
    stage('Builds') {
      parallel {
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
      }
    }
    stage('Archive Artifacts') {
      steps {
        archiveArtifacts 'backend/target/*.jar'
        archiveArtifacts 'frontend/dist/*'
      }
    }
    stage('Docker Compose') {
      steps {
        echo 'Building Docker'
        sh 'docker-compose up -d --build'
      }
    }
    stage('Testing the APP') {
      steps {
        echo 'Running test cases'
        sh '/usr/bin/curl http://localhost:4200'
      }
    }
    stage('Final Step') {
      steps {
        input 'Finished using the web site? (Click "Proceed" to continue)'
      }
    }
  }
  post {
    always {
      sh 'docker-compose down'

    }

  }
}