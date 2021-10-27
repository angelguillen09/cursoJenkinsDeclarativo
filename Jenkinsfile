node {
    stage('Etapa 0'){
        echo 'Dentro de la Etapa 0'
    }
    stage('Etapa 1'){
        try{
            echo 'Dentro de la Etapa 1'
            // Esta tarea se ejecura siempre que las anteriores hayan ido bien
            echo 'Despues de la Etapa 1, si va bien'
        }catch (exc){
            // Este seria el caso failure del Declarativo
            echo 'Esto solo se va a ejecutar si se ha producido un error'   
        }finally {
            echo 'Esto se ejecuta si hay error o no'   
        }
        echo 'Luego vendrían más tareas después.'
    }
}