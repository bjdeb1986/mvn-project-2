pipeline{
    agent{
        node{
            label 'agent01'
        }
    }
    tools{
        maven 'maven-3.3.1'
    }
    options{
        buildDiscarder(logRotator(numToKeepStr: '5'))
        disableResume()
        disableConcurrentBuilds()
        timestamps()
        timeout(time: 1, unit: 'HOURS')
    }
    stages{
        stage('Pre Check'){
            steps{
                sh 'mvn --version'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Execute'){
            steps{
                sh 'java -cp ${WORKSPACE}/target/mvn-project-2-1.0.jar myTest.com.App'
            }
        }
    }
    post{
        always{
            echo "Archiving Artifacts"
            archiveArtifacts allowEmptyArchive: false, artifacts: 'target/*.jar', defaultExcludes: false, fingerprint: true, followSymlinks: false, onlyIfSuccessful: true
        }
        cleanup{
            echo "Cleaning up working directory"
            cleanWs()
        }
    }
}
