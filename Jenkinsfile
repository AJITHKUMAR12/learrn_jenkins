pipeline {
    agent any

    stages {
        stage('build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                    args '-u root' // Run the container as root
                }
            }
            steps {
                sh '''
                ls -la
                npm ci
                npm run build
                ls -l
                '''
            }
        }
        stage('test'){
              agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                    args '-u root' // Run the container as root
                }
            }
            steps{
                sh '''
                test -f build/index.html
                npm test
                '''
            }
        }
    }
    post{
        always{
            junit 'test-results/junit.xml'
        }
    }
   

        
    
}
