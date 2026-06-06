# Gantt, Grafo y Camino Crítico

Este documento contiene las tres piezas clave de la planificación del proyecto: el grafo de dependencias, el diagrama de Gantt y el análisis del camino crítico.

## 1. Tareas del proyecto

| Código | Tarea | Duración | Predecesores |
|---|---|---|---|
| T1.1 | Chasis y Motores | 5 días | - |
| T1.2 | Sensores y SBC | 7 días | - |
| T1.3 | Sistema de Potencia | 4 días | T1.1 |
| T1.4 | Ensamblado y Cableado | 6 días | T1.2, T1.3 |
| T2.1 | Firmware Motores | 5 días | T1.4 |
| T2.2 | Comunicación SBC-MCU | 4 días | T2.1 |
| T2.3 | Teleoperación y Grabación | 3 días | T2.2 |
| T3.1 | Configuración ROS2 | 2 días | T1.2 |
| T3.2 | Integración LiDAR | 3 días | T3.1 |
| T3.3 | SLAM y Odometría | 6 días | T3.2, T2.2 |
| T3.4 | Nav2 y Playback | 8 días | T3.3, T2.3 |
| T4.1 | Cámara y OpenCV | 2 días | T3.1 |
| T4.2 | Modelo de Detección | 7 días | T4.1 |
| T4.3 | E-Stop / Evitación | 5 días | T4.2, T3.4 |
| T5.1 | Integración de Software | 4 días | T4.3 |
| T5.2 | Pruebas Controladas | 4 días | T5.1 |
| T5.3 | Pruebas de Campo | 5 días | T5.2 |
| T5.4 | Documentación y Cierre | 3 días | T5.3 |

## 2. Grafo de dependencias

```mermaid
graph TD
    classDef critical fill:#ffebee,stroke:#c62828,stroke-width:3px,color:#b71c1c;
    classDef normal fill:#e1f5fe,stroke:#0288d1,stroke-width:1.5px,color:#01579b;

    T1_1["T1.1: Chasis y Motores (5d)"]:::critical
    T1_2["T1.2: Sensores y SBC (7d)"]:::normal
    T1_3["T1.3: Sistema de Potencia (4d)"]:::critical
    T1_4["T1.4: Ensamblado y Cableado (6d)"]:::critical
    T2_1["T2.1: Firmware Motores (5d)"]:::critical
    T2_2["T2.2: Comunicación SBC-MCU (4d)"]:::critical
    T2_3["T2.3: Teleoperación y Grabación (3d)"]:::normal
    T3_1["T3.1: Configuración ROS2 (2d)"]:::normal
    T3_2["T3.2: Integración LiDAR (3d)"]:::normal
    T3_3["T3.3: SLAM y Odometría (6d)"]:::critical
    T3_4["T3.4: Nav2 y Playback (8d)"]:::critical
    T4_1["T4.1: Cámara y OpenCV (2d)"]:::normal
    T4_2["T4.2: Modelo de Detección (7d)"]:::normal
    T4_3["T4.3: E-Stop / Evitación (5d)"]:::critical
    T5_1["T5.1: Integración de Software (4d)"]:::critical
    T5_2["T5.2: Pruebas Controladas (4d)"]:::critical
    T5_3["T5.3: Pruebas de Campo (5d)"]:::critical
    T5_4["T5.4: Doc. y Cierre (3d)"]:::critical

    T1_1 --> T1_3
    T1_2 --> T1_4
    T1_3 --> T1_4
    T1_4 --> T2_1
    T2_1 --> T2_2
    T2_2 --> T2_3
    T2_2 --> T3_3
    T1_2 --> T3_1
    T3_1 --> T3_2
    T3_1 --> T4_1
    T3_2 --> T3_3
    T2_3 --> T3_4
    T3_3 --> T3_4
    T4_1 --> T4_2
    T4_2 --> T4_3
    T3_4 --> T4_3
    T4_3 --> T5_1
    T5_1 --> T5_2
    T5_2 --> T5_3
    T5_3 --> T5_4

    linkStyle 0,2,3,4,6,12,15,16,17,18,19 stroke:#c62828,stroke-width:3px;
```

## 3. Diagrama de Gantt

```mermaid
%%{init: { 'gantt': { 'tickInterval': '2d' } } }%%
gantt
    title Cronograma LawnMowerBot (Robot Cortacésped) - 59 Días Totales
    dateFormat YYYY-MM-DD
    axisFormat %d-%b
    tickInterval 2d

    section Fase 1: Hardware
    T1.1 - Diseño Chasis (Días 1-5)            :active, t1_1, 2026-06-03, 5d
    T1.2 - Adquisición Sensores (Días 1-7)     :t1_2, 2026-06-03, 7d
    T1.3 - Sistema de Potencia (Días 6-9)      :t1_3, after t1_1, 4d
    T1.4 - Ensamblado Mecánico (Días 10-15)    :t1_4, after t1_3, 6d

    section Fase 2: Bajo Nivel
    T2.1 - Firmware Motores (Días 16-20)       :t2_1, after t1_4, 5d
    T2.2 - Comunicación SBC-MCU (Días 21-24)   :t2_2, after t2_1, 4d
    T2.3 - Teleoperación y Grabación (Días 25-27):t2_3, after t2_2, 3d

    section Fase 3: ROS 2 / SLAM
    T3.1 - OS y ROS2 en SBC (Días 8-9)         :t3_1, after t1_2, 2d
    T3.2 - Integración LiDAR (Días 10-12)      :t3_2, after t3_1, 3d
    T3.3 - Odometría y Mapeo SLAM (Días 25-30) :t3_3, after t2_2, 6d
    T3.4 - Navegación y Playback (Días 31-38)  :t3_4, after t3_3, 8d

    section Fase 4: Visión (RGB)
    T4.1 - Cámara y OpenCV (Días 10-11)        :t4_1, after t3_1, 2d
    T4.2 - Modelo Detección (Días 12-18)       :t4_2, after t4_1, 7d
    T4.3 - E-Stop y Evitación (Días 39-43)     :t4_3, after t3_4, 5d

    section Fase 5: Integración
    T5.1 - Integración Software (Días 44-47)   :t5_1, after t4_3, 4d
    T5.2 - Pruebas Controladas (Días 48-51)    :t5_2, after t5_1, 4d
    T5.3 - Pruebas de Campo (Días 52-56)       :t5_3, after t5_2, 5d
    T5.4 - Doc. y Cierre (Días 57-59)          :t5_4, after t5_3, 3d
```

## 4. Análisis del camino crítico

El camino crítico es la secuencia de tareas que determina la duración mínima del proyecto. Si alguna de estas tareas se retrasa, el proyecto se atrasará.

### Tareas en el camino crítico

- T1.1: Chasis y Motores
- T1.3: Sistema de Potencia
- T1.4: Ensamblado y Cableado
- T2.1: Firmware Motores
- T2.2: Comunicación SBC-MCU
- T3.3: SLAM y Odometría
- T3.4: Nav2 y Playback
- T4.3: E-Stop / Evitación
- T5.1: Integración de Software
- T5.2: Pruebas Controladas
- T5.3: Pruebas de Campo
- T5.4: Documentación y Cierre

### Tabla de tiempos y holguras

| Código | Tarea | Duración | Holgura | Crítico |
|---|---|---|---|---|
| T1.1 | Chasis y Motores | 5 | 0 | Sí |
| T1.2 | Sensores y SBC | 7 | 2 | No |
| T1.3 | Sistema de Potencia | 4 | 0 | Sí |
| T1.4 | Ensamblado y Cableado | 6 | 0 | Sí |
| T2.1 | Firmware Motores | 5 | 0 | Sí |
| T2.2 | Comunicación SBC-MCU | 4 | 0 | Sí |
| T2.3 | Teleoperación y Grabación | 3 | 3 | No |
| T3.1 | Configuración ROS2 | 2 | 12 | No |
| T3.2 | Integración LiDAR | 3 | 12 | No |
| T3.3 | SLAM y Odometría | 6 | 0 | Sí |
| T3.4 | Nav2 y Playback | 8 | 0 | Sí |
| T4.1 | Cámara y OpenCV | 2 | 20 | No |
| T4.2 | Modelo Detección | 7 | 20 | No |
| T4.3 | E-Stop / Evitación | 5 | 0 | Sí |
| T5.1 | Integración de Software | 4 | 0 | Sí |
| T5.2 | Pruebas Controladas | 4 | 0 | Sí |
| T5.3 | Pruebas de Campo | 5 | 0 | Sí |
| T5.4 | Documentación y Cierre | 3 | 0 | Sí |

## 5. Cómo usar esto en tu entrega

- Si necesitas un documento de planificación, copia este archivo completo.
- Si necesitas sólo el Gantt y el grafo, usa las secciones 2 y 3.
- Si necesitas explicar el camino crítico, usa la sección 4.
- Puedes pegar esto directamente en tu informe o presentación.
