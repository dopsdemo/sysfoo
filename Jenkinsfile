pipeline {
<<<<<<< HEAD

  agent any

  tools{
     maven 'Maven 3.6.3'
  }

  stages {
     stage('build'){
        steps{
          echo 'compiling sysfoo app'
          sh 'mvn compile'
        }
     }

    stage('test'){
       steps{
         echo 'unit testing sysfoo app'
         sh 'mvn clean test'
        }
     }

     stage('package'){
        steps{
          echo 'packaging sysfoo app'
          sh 'mvn package -DskipTests'
        }
     }

  }

}
=======
  agent any
  stages {
    stage('build') {
      steps {
        echo 'compiling sysfoo app'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'unit testing sysfoo app'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      steps {
        echo 'packaging sysfoo app'
        sh 'mvn package -DskipTests'
        archiveArtifacts 'target/*.war'
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
}
>>>>>>> 86a8a2cc15197accf9a16ff3e5be1f14e43d36e9
