pipeline {
  agent any
  stages {
    stage('Builds') {
      parallel {
        stage('Build Backend') {
          agent {
            docker {
              image 'maven'
            }

          }
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
  }
  post {
    always {
      sh 'docker-compose down'

    }

  }
}