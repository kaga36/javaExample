pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }

    stage('Compile') {
      steps {
        sh '''
          set -eux
          java -version || true
          javac -version || true

          mkdir -p out
          find src -name "*.java" -print
          javac -d out $(find src -name "*.java")

          echo "---- classes ----"
          find out -name "*.class" -print
        '''
      }
    }

    stage('Run') {
      steps {
        sh '''
          set -eux
          # main 클래스가 javaExample.Hello라면 아래처럼
          java -cp out javaExample.Hello
        '''
      }
    }

      stage('Archive classes') {
      steps {
        archiveArtifacts artifacts: 'out/**/*.class', fingerprint: true
      }
    }
  }
}
