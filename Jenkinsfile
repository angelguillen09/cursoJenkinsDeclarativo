pipeline {
    agent any
    
    stages{
        stage('Etapa 1'){
            steps {
                echo 'Dentro de Etapa 1'
            }
        }
        stage('Etapa 2'){
            steps {
                echo 'Dentro de Etapa 2'
               
            }
        }
        stage('Etapa 3'){
            steps {
                echo 'dentro de Etapa 3'
                
            }
            post {
                
            }
        }
    }
    post {
        always {
            echo 'dentro de Etapa 3'
            
        }
        success {
            echo 'dentro de Etapa 3'
            
        }
        failure {
            echo 'dentro de Etapa 3'
        }
    }
}
