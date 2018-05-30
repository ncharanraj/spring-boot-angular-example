pipeline {
    agent any 
    environment{
        JAVA_HOME = "/usr/lib/jvm/java-1.8.0"
    }
    stages {
        stage('Builds'){
            parallel{
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
        }
    }
}