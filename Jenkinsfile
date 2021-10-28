VERSION_DEL_PIPELINE="1"

if (this.params.getOrDefault('VERSION_DEL_PIPELINE',"-1")!=VERSION_DEL_PIPELINE){
    creoConfiguracion()
    return
}

node {
    stage ("Etapa 1") {
        echo "Hago mis cosas"
    }
    stage ("Etapa 2") {
        echo "Hago más de mis cosas"
    }
}

def creoConfiguracion(){
    properties(
        [
            parameters(
                [
                    choice(name: 'VERSION_DEL_PIPELINE', description: 'Version del pipeline instalada', choices: [ VERSION_DEL_PIPELINE ])
                    // Aqui pongo el resto de params que necesite mi pipeline
                ]
            )
        ]
    )
}

