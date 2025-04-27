pipeline {
    agent none

    stages {
        stage('Maven Install') {
            agent {
                docker {
                    image 'maven:3.9.6'
                    args '-v $HOME/.m2:/root/.m2' // Montar el repositorio local de Maven para cachear dependencias
                }
            }
            steps {
                script {
                    try {
                        sh 'mvn clean install'
                    } catch (err) {
                        error "Maven build failed: ${err}"
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
        always {
            echo 'Cleaning up...'
            cleanWs()
        }
    }
}
