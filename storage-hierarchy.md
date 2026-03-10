flowchart TD
    subgraph UserSpace ["🖥️ Capa de Usuario (User Space)"]
        direction LR
        App1([Aplicación de Usuario])
        App2([Navegador Web])
        App3([Terminal / Shell])
        Lib[[Bibliotecas del Sistema / API]]
        
        App1 & App2 & App3 --> Lib
    end

    subgraph KernelSpace ["⚙️ Capa del Núcleo (Kernel Space)"]
        direction TB
        SCI{Interfaz de Llamadas al Sistema}
        
        subgraph SubSistemas ["Componentes Principales del SO"]
            direction LR
            PM[Gestión de Procesos]
            MM[Gestión de Memoria]
            FS[Sistema de Archivos]
            IO[Gestión de E/S]
            Net[Subsistema de Red]
        end
        
        SCI --> PM & MM & FS & IO & Net
        Drivers[(Controladores de Dispositivos / Drivers)]
        
        PM & MM & FS & IO & Net --> Drivers
    end

    subgraph HW ["🖧 Capa de Hardware"]
        direction LR
        CPU[Procesador / CPU]
        RAM[Memoria Principal]
        Disk[Discos / SSD]
        Periph[Periféricos]
    end

    Lib -->|System Calls| SCI
    Drivers <-->|Interrupciones y Comandos| HW

    %% Estilos Modernos
    classDef userLayer fill:#eef2ff,stroke:#6366f1,stroke-width:2px,color:#312e81;
    classDef kernelLayer fill:#f0fdf4,stroke:#22c55e,stroke-width:2px,color:#14532d;
    classDef hwLayer fill:#fffbeb,stroke:#f59e0b,stroke-width:2px,color:#78350f;
    
    class UserSpace userLayer;
    class KernelSpace kernelLayer;
    class HW hwLayer;
