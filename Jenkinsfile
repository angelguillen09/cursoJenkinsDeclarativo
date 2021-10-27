// Puedo definir un parametro, donde me de la gana del fichero !!!!
// EUREKA !!!!
properties (
    [
        parameters(
                [
                    string(defaultValue: '1', name: 'CODIGO_SALIDA')
                ]
            ),
        pipelineTriggers(
                [
                    cron("* * * * *")
                ]
            )
    ]    
)

node {
    stage('Etapa 0'){
        echo 'Dentro de la Etapa 0'
    }
    try{
        stage('Etapa 1'){
            try{
                echo 'Dentro de la Etapa 1'
                if (this.params.CODIGO_SALIDA != "0") {
                    sh 'exit 1'
                }
                // Esta tarea se ejecura siempre que las anteriores hayan ido bien
                echo 'Despues de la Etapa 1, si va bien'
            }catch (exc){
                // Este sería el caso del catchError
                echo 'Esto solo se va a ejecutar si se ha producido un error'   
                // Este seria el caso failure del Declarativo
                throw exc
            }finally {
                echo 'Esto se ejecuta si hay error o no'   
            }
            echo 'Luego vendrían más tareas después.'
        }
    } catch (exc) {
        echo 'Esto se ejecutaría si en algun sitio de etapa 1 ha habido un error'
    } finally {
        echo 'Esto se ejecutaría independientemente de si la etapa 1 ha ido bien o no.'
    }
    stage('Etapa 2'){
        echo 'Estoy en la etapa 2'   
    }
    stage('Etapa 3'){
        echo 'Estoy en la etapa 3'   
        parallel (
            "Subetapa 3.1": {
                stage('Etapa 3.1'){
                    echo 'Estoy en la etapa 3.1'   
                    sh 'sleep 10'
                }
            },
            "Subetapa 3.2": {
                stage('Etapa 3.2'){
                    echo 'Estoy en la etapa 3.2'   
                    sh 'sleep 10'
                }
            }
        )
    }

    stage('Etapa 4'){
        so = ['Linux','Macos','BSD']
        programas = ['nginx','apache']
        
        for (int i=0;i<so.size();i++){
            for (int j=0;j<programas.size();j++){
                if (so[i]=='Linux' && programas[j]=='apache'){
                    continue
                }
                echo "Voy a probar mi app sobre ${so[i]} corriendo en ${programas[j]}"
            }
        }
    }
    
}