pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'rm -rf build'
                input('Do you want to proceed?')
                sh 'mkdir build'
                sh 'touch build/car.txt'
                sh 'echo "chassis" >> build/car.txt'
                sh 'echo "engine" >> build/car.txt'
                sh 'echo "body" >> build/car.txt'
            }
        }
        stage('Test') {
            steps {
                sh 'test -f build/car.txt'
                sh 'grep "chassis" build/car.txt'
                sh 'grep "engine" build/car.txt'
                sh 'grep "body" build/car.txt'
            }
        }
            
        stage('Publish') {
            steps {
                archiveArtifacts artifacts: 'build/'
            }
        }
    }
    post {
        always {
            echo 'This will alwals run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echi 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
