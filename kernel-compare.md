```mermaid
flowchart TD
    subgraph Monolithic ["Arquitectura Monolítica (Monolithic)"]
        direction TB
        M_User["🖥️ Capa de Usuario
        (Aplicaciones)"]
        
        subgraph M_Kernel ["⚙️ Capa del Núcleo (Todo Integrado)"]
            direction TB
            M_FS[Sistema de Archivos]
            M_IPC[Comunicación entre Procesos]
            M_Mem[Gestión de Memoria]
            M_Drivers[Controladores de Dispositivos]
        end
        
        M_HW["🖧 Capa de Hardware"]
        
        M_User -->|System Calls| M_Kernel
        M_Kernel --> M_HW
    end

    subgraph Microkernel ["Arquitectura Micronúcleo (Microkernel)"]
        direction TB
        
        subgraph u_User ["🖥️ Capa de Usuario (Servicios Separados)"]
            direction TB
            u_App["Aplicaciones de Usuario"]
            u_FS["Servidor de Archivos"]
            u_Drivers["Servidor de Controladores"]
            u_Net["Servidor de Red"]
        end
        
        subgraph u_Kernel ["⚙️ Capa del Núcleo (Mínima)"]
            direction LR
            u_IPC[IPC Básico / Mensajes]
            u_Mem[Memoria Virtual Básica]
            u_Sched[Planificación de CPU]
        end
        
        u_HW["🖧 Capa de Hardware"]
        
        u_User <-->|Mensajes IPC| u_Kernel
        u_Kernel --> u_HW
    end

    %% Estilos
    classDef userLayer fill:#eef2ff,stroke:#6366f1,stroke-width:2px,color:#312e81;
    classDef kernelLayer fill:#f0fdf4,stroke:#22c55e,stroke-width:2px,color:#14532d;
    classDef hwLayer fill:#fffbeb,stroke:#f59e0b,stroke-width:2px,color:#78350f;
    classDef monoKernel fill:#fee2e2,stroke:#ef4444,stroke-width:2px,color:#7f1d1d;
    
    class M_User,u_User,u_App,u_FS,u_Drivers,u_Net userLayer;
    class M_Kernel monoKernel;
    class u_Kernel kernelLayer;
    class M_HW,u_HW hwLayer;
