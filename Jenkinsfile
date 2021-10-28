// Plantilla de PIPELINE.
// Autor: IvanciniGT

// Al cambiar la verisón sólo se recarga la configuración del proyecto... pero no se ejecutarán las tareas
VERSION_DEL_PIPELINE="0"

// Añadir aquí los parámetros del pipeline
PARAMETROS_DE_MI_PIPELINE=[
    // booleanParam (defaultValue: true, description: 'Descripción de mi parámetro', name: 'MI_PARAM_BOOLEAN'),
    // string(defaultValue: 'valor por defecto', description: 'Descripción de mi parámetro de texto', name: 'MI_PARAM_TEXTO'),
    // choice(choices: ['Valor1', 'Valor2', 'Valor3'], description: 'Descripción de mi parámetro', name: 'MI_PARAM_LISTA')
]

// Añadir aquí los parámetros del pipeline
TRIGGERS_DE_MI_PIPELINE=[
    //cron("* * * * *"),                                                        // Ejecutar cada minuto
    //pollSCM("* * * * *")                                                      // Ejecutar cuando cambie algo en GIT
    //upstream(upstreamProjects: 'PROYECTO_DISPARADOR', threshold: 'FAILURE')   // Ejecutar tras otro proyecto (Incluso si falla)
]

// No tocar este trozo... es el que hace la magia
if (this.params.getOrDefault('VERSION_DEL_PIPELINE',"-1")!=VERSION_DEL_PIPELINE){
    stage('Configuración del JOB'){
        creoConfiguracion()
    }
    return
}
// Aquí empiezan las tareas propias de mi pipeline
node {
    try{
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
        
    }
    finally {
        //stage ("Limpieza del workspace") {
        //    cleanWs()
        //}
    }
}
// Función que crea la configuración. NO TOCAR si no sabes lo que estás haciendo ;)
def creoConfiguracion(){
    properties(
        [
            parameters(
                [
                    choice(name: 'VERSION_DEL_PIPELINE', description: 'Version del pipeline instalada', choices: [ VERSION_DEL_PIPELINE ])
                ] + PARAMETROS_DE_MI_PIPELINE
            ),
            pipelineTriggers( TRIGGERS_DE_MI_PIPELINE )
        ]
    )
}