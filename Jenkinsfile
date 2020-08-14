pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Build & Test') {
      agent {
        node {
          label 'docker'
        }

      }
      steps {
        dir(path: 'Ch03/example-maven-project') {
          sh '''


mvn -Dmaven.test.failure.ignore clean package'''
        }

        stash(name: 'build-test-artifacts', includes: '**/Ch03/example-maven-project/target/surefire-reports/TEST-*.xml,target/*.jar')
      }
    }

    stage('Report & Publish') {
      agent {
        node {
          label 'docker'
        }

      }
      steps {
        unstash 'build-test-artifacts'
        junit '**/Ch03/example-maven-project/target/surefire-reports/TEST-*.xml'
        archiveArtifacts(artifacts: 'Ch03/example-maven-project/target/*.jar', onlyIfSuccessful: true)
      }
    }

  }
}