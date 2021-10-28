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
// No tocar este trozo... es el que hace la magia
if (this.params.getOrDefault('VERSION_DEL_PIPELINE',"-1")!=VERSION_DEL_PIPELINE){
    stage('Configuración del JOB'){
        creoConfiguracion()
    }
    return
}
// Aquí empiezan las tareas propias de mi pipeline
node {
    stage ("Etapa 1") {
        echo "Hago mis cosas"
    }
    stage ("Etapa 2") {
        echo "Hago más de mis cosas"
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
            )
        ]
    )
}