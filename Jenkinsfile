pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'apicambiosmonedatt'
        CONTAINER_NAME = 'dockerapiCambiosmonedatt'
        APP_PORT = '5235'
        HOST_PORT = '7080'
        DOCKER_NETWORK = 'dockermonedas_red'
    }
    stages {
        steps('ejecutar pruebas unitarias'){
            script{
                bat "dotnet test apiCambiosMoneda.Test\\apiCambiosMoneda.Test.csproj --configuration Release"
            }
        }
        stage ('Construir imagen Docker'){
            steps {
                bat "docker build . -t ${DOCKER_IMAGE}"

            }
        }
        stage('Limpiar contenedor existente') {
            steps {
                bat "docker rm -f ${DOCKER_NETWORK} || exit 0"
                }
            }
        }
         stage('Ejecutar contenedor') {
            steps {
                bat "docker run --network ${DOCKER_NETWORK} --name ${CONTAINER_NAME} -p ${HOST_PORT}:${CONTAINER_PORT} -d ${DOCKER_IMAGE}"
            }
        }
    }

}
