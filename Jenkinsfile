pipeline {
    agent any
    
    stages{
        stage('Etapa 1'){
            steps {
                echo 'Dentro de la Etapa 1'
            }
            post {
                success {
                    echo 'Despues de la Etapa 1, si va bien'
                }
            }
        }
        stage('Etapa 2'){
            stages {                                    // Me ayuda a tener el trabajo más organizado
                stage('Etapa 2.1') {
                    steps {
                        echo 'Dentro de la Etapa 2.1'
                    }
                    //post {}
                }
                stage('Etapa 2.2') {
                    steps {
                        catchError(buildResult: 'SUCCESS', message: 'Aqui la cagamos !!!!!', stageResult: 'FAILURE') {
                            echo 'Dentro de la Etapa 2.2'
                            echo 'Esta etapa genera una explosión gigantescamente aberrante !!!! ;)'
                            sh 'exit 1'
                        }
                    }
                    post {
                        success {
                            echo 'La Etapa 2.2 acabó guay'
                        }
                        failure {
                            echo 'La Etapa 2.2 acabó fatalmente mal'
                        }
                        always {
                            echo 'La Etapa 2.2 acabó !!!!'
                        }
                    }
                }
                stage('Etapa 2.3') {
                    steps {
                        echo 'Dentro de la Etapa 2.3'
                    }
                    //post {}
                }
            }
            //post {}
        }
        stage('Etapa 3'){
            parallel {
                stage('Etapa 3.1'){
                    steps {
                        sh 'sleep 10'
                    }
                }
                stage('Etapa 3.2'){
                    steps {
                        sh 'sleep 10'
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Al acabar siempre'
        }
        success {
            echo 'Al acabar si todo ha ido bien'
        }
        failure {
            echo 'Al acabar si algo ha ido mal'
        }
    }
}