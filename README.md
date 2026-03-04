# Proyecto Digimon SOA - ACT6-C2

Este proyecto implementa una arquitectura desacoplada para consultar la Digimon API. Se divide en tres componentes principales que deben ser tratados como repositorios independientes.

## Estructura del Proyecto

-   **/frontend**: Aplicación Next.js (TypeScript + Tailwind) que consume el Backend Proxy.
-   **/backend**: Servidor Node.js (Express + TypeScript) que sirve como Proxy para la Digimon API externa.
-   **/infrastructure**: Configuración de Docker Compose para orquestar ambos servicios.
-   **/docs**: Documentación técnica y diagramas de arquitectura.

## Inicio Rápido

Para levantar todo el sistema:

1.  Asegúrate de tener Docker instalado.
2.  Navega a la carpeta de infraestructura:
    ```bash
    cd infrastructure
    ```
3.  Levanta los servicios:
    ```bash
    docker-compose up --build
    ```

## Documentación Detallada

Consulta el archivo de [Arquitectura](./docs/architecture.md) para ver los diagramas y la justificación técnica.
