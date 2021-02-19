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
            parallel{
                stage('Tests 1') {
                    steps {
                        sh 'test -f build/car.txt'
                        sh 'grep "chassis" build/car.txt'
                        sh 'grep "engine" build/car.txt'
                        sh 'grep "body" build/car.txt'
                    }
                }
                stage('Tests 2') {
                    agent {
                        docker{
                            reuseNode false
                            image 'ubuntu'
                        }
                    }
                    steps {
                        echo 'Running the integration tests...'                        
                    }
                }
            }
         }
            
        stage('Publish') {
            steps {
                archiveArtifacts artifacts: 'build/'
            }
        }
    }
}
