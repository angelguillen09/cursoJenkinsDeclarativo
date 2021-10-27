pipeline {
    agent {
        docker {
            image 'ubuntu'
        }
        //dockerfile
    }
    
    parameters {   // Dando de alta un parametro que se solicitará al ejecutar un proyecto
      string defaultValue: '0', name: 'CODIGO_SALIDA'
    }
    
        
    stages{
        stage('Etapa 0'){
            steps {
                echo 'Dentro de la Etapa 0'
                // Previamente habriamos añado un trigger de forma que si hay un cambio en el repo, se ejecute autom el job
                // ESTA ES MUY CUTRE... ESTA NO LA QUEREMOS. Si es la primera ejecución, solo dar de alta parametros
                // Comprobar si ha habido un cambio en el fichero Jenkinsfile del repo
                // Se corte la ejecución del JOB
            }
        }
        stage('Etapa 1'){
            steps {
                echo 'Dentro de la Etapa 1'
                sh 'hostname'
                sh 'pwd'
                sh 'ls -l'
                sh 'ls -l /'
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
                            sh "exit ${CODIGO_SALIDA}"
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
        stage('Etapa en matriz') {
            matrix {
                axes {
                    axis {
                        name 'SISTEMA_OPERATIVO'
                        values 'Linux','Macos','BSD'
                    }
                    axis {
                        name 'PROGRAMA'
                        values 'nginx','apache'
                    }
                }
                excludes {
                    exclude {
                        axis {
                            name 'SISTEMA_OPERATIVO'
                            values 'Linux'
                        }
                        axis {
                            name 'PROGRAMA'
                            values 'apache'
                        }
                    }
                }
                stages {
                    stage('Probar el sistema') {
                        steps {
                            echo "Voy a probar mi app sobre ${SISTEMA_OPERATIVO} corriendo en ${PROGRAMA}"
                        }
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