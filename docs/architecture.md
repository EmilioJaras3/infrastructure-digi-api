# Arquitectura del Sistema - Digimon SOA

Este documento detalla el diseño de la **Arquitectura Orientada a Servicios (SOA)** implementada para la exposición y consumo de la Digimon API.

## Diagrama de Arquitectura

```mermaid
graph TD
    subgraph "Frontend Layer (Port 3000)"
        UI[User Interface - Next.js]
        Hooks[Custom Hooks - Fetch/Async]
    end

    subgraph "Backend Layer (Port 4000)"
        Proxy[Proxy API - Express]
        Service[Service Layer - Axios]
    end

    subgraph "External API"
        DigimonAPI[Digimon API v1]
    end

    subgraph "Infrastructure"
        Docker[Docker Compose]
        Net[Virtual Network]
    end

    UI --> Hooks
    Hooks --> Proxy
    Proxy --> Service
    Service --> DigimonAPI
    Docker --> UI
    Docker --> Proxy
    Net --- UI
    Net --- Proxy
```

## Justificación Técnica

La arquitectura se diseñó bajo el principio de **desacoplamiento estricto**, cumpliendo con los requisitos de la actividad ACT6-C2:

1.  **Independencia de Repositorios:** El Frontend, el Backend y la Infraestructura residen en carpetas separadas que pueden ser gestionadas como repositorios independientes.
2.  **Capa de Proxy:** El Backend actúa como un mediador que protege al cliente de llamadas directas a APIs de terceros, permitiendo agregar lógica de seguridad, caché o transformación de datos en el futuro.
3.  **Aislamiento de Entorno:** Mediante Docker, cada capa corre en su propio contenedor con puertos aislados, comunicándose a través de una red virtual interna.
4.  **Manejo Asíncrono:** Toda la comunicación entre capas utiliza `async/await`, garantizando que la UI no se bloquee mientras espera respuestas.
5.  **Separación de Responsabilidades:**
    *   **Frontend:** Solo visualización y estado de UI.
    *   **Backend:** Lógica de negocio y conectividad externa.
    *   **Infraestructura:** Orquestación y despliegue.
