import groovy.json.*


LOGGER = new StringBuilder()

properties([
        parameters([
            choice(name: 'org', choices: ['onpremDev', 'awsQA', 'onpremProd'], description: ''),
            booleanParam(name: 'Migrar', defaultValue: false,  description: ''),
            booleanParam(name: 'cleanWokspace', defaultValue: false,  description: ''),
            string(name: 'apiName', defaultValue: '', description: 'Nombre del API proxy a migrar'),
        ])
    ])

try {
    print("Organización seleccionada: \"$params.org\"")
    if(params.cleanWokspace){
        print("Limpiando Workspace....")
        deleteDir()
    }
    if (params.Migrar){
        if(params.apiName.contains(',')){
            params.apiName.split(",").each{    apiProxy ->
                main(apiProxy.trim())
            }
        }
        else{
            main(params.apiName.trim())
        }
        String logger = LOGGER.toString()
        String notdeployed = NOTDEPLOYED.toString()
        print('******************** RESUMEN *****************************')
        print("API Proxies desplegados en el cluster destino \"${prettyFQDN(fqdnDestination)}\"")
        print(logger)
        print('**********************************************************')
        print("API Proxies no desplegados en el cluster destino \"${prettyFQDN(fqdnDestination)}\"")
        print(notdeployed)
    } else {
        print("Parametro 'Migrar' no seleccionado.")
    }
}
catch (err) {
    currentBuild.result = 'FAILED'
    throw err
}

def main(String apiProxy){
    print("Iniciando proceso de migración...")
    print("Finishing")
}
