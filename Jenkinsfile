pipeline {
  agent none
  stages {
    stage('build') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'compiling sysfoo app'
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'unit testing sysfoo app'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      when {         
             beforeAgent true
             branch  'master' 
           }

      agent {
        docker {
          image 'maven:3.6.3-jdk-11-slim'
        }

      }
      steps {
        echo 'packaging sysfoo app'
        sh 'mvn package -DskipTests'
        archiveArtifacts 'target/*.war'
      }
    }

    stage('Docker BnP') {
      agent any 
      when {
             beforeAgent true
             branch  'master'
           }
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
            def dockerImage = docker.build("initcron/sysfoo:v${env.BUILD_ID}", "./")
            dockerImage.push()
            dockerImage.push("latest")
            dockerImage.push("dev")
          }
        }

      }
    }

    stage('Deploy to Dev') {
      when {
             beforeAgent true
             branch  'master'
           }

      agent any

      steps {
        echo 'Deploying to Dev Environment with Docker Compose'
        sh 'docker-compose up -d'
      }
    }

  }
}
