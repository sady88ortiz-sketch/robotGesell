# Planificación del Proyecto: Cortadora de Pasto Semi-Autónoma

Este documento organiza el trabajo del proyecto en tareas, dependencias y cronograma.

## Estructura del trabajo (WBS)

| Código | Tarea | Duración | Predecesores |
|---|---|---|---|
| T1.1 | Diseño del chasis | 5 días | - |
| T1.2 | Selección de componentes | 4 días | T1.1 |
| T1.3 | Diseño eléctrico y de potencia | 3 días | T1.1 |
| T1.4 | Ensamblado mecánico | 5 días | T1.2, T1.3 |
| T2.1 | Firmware motores y encoders | 5 días | T1.4 |
| T2.2 | Comunicación SBC-MCU | 4 días | T2.1 |
| T3.1 | Configuración de ROS2 / software | 3 días | T1.2 |
| T3.2 | Integración de sensores LiDAR/cámara | 4 días | T3.1 |
| T3.3 | Odometría y mapeo | 6 días | T2.2, T3.2 |
| T3.4 | Navegación Teach-and-Repeat | 6 días | T3.3 |
| T4.1 | Visión y detección de obstáculos | 5 días | T3.1 |
| T4.2 | E-Stop y seguridad | 4 días | T4.1, T3.4 |
| T5.1 | Integración final | 4 días | T4.2 |
| T5.2 | Pruebas y ajustes | 5 días | T5.1 |
| T5.3 | Documentación final | 3 días | T5.2 |

## Diagrama de Gantt

```mermaid
%%{init: { 'gantt': { 'tickInterval': '2d' } } }%%
gantt
    title Cronograma Proyecto Cortacésped - 54 Días Estimados
    dateFormat  YYYY-MM-DD
    axisFormat  %d-%b

    section Fase 1: Diseño y Hardware
    Diseño del chasis              :t1_1, 2026-06-05, 5d
    Selección de componentes       :t1_2, after t1_1, 4d
    Diseño eléctrico y potencia    :t1_3, after t1_1, 3d
    Ensamblado mecánico            :t1_4, after t1_2, 5d

    section Fase 2: Firmware
    Firmware motores y encoders    :t2_1, after t1_4, 5d
    Comunicación SBC-MCU           :t2_2, after t2_1, 4d

    section Fase 3: Software de Navegación
    Configuración de ROS2/Software :t3_1, after t1_2, 3d
    Integración sensores           :t3_2, after t3_1, 4d
    Odometría y mapeo              :t3_3, after t2_2, 6d
    Navegación Teach-and-Repeat    :t3_4, after t3_3, 6d

    section Fase 4: Visión y Seguridad
    Visión y detección             :t4_1, after t3_1, 5d
    E-Stop y seguridad             :t4_2, after t4_1, 4d

    section Fase 5: Integración y Cierre
    Integración final              :t5_1, after t4_2, 4d
    Pruebas y ajustes              :t5_2, after t5_1, 5d
    Documentación final            :t5_3, after t5_2, 3d
```

## Camino crítico

Las tareas críticas son aquellas que no tienen holgura y determinan la duración mínima del proyecto.

- T1.1 Diseño del chasis
- T1.2 Selección de componentes
- T1.4 Ensamblado mecánico
- T2.1 Firmware motores y encoders
- T2.2 Comunicación SBC-MCU
- T3.3 Odometría y mapeo
- T3.4 Navegación Teach-and-Repeat
- T4.2 E-Stop y seguridad
- T5.1 Integración final
- T5.2 Pruebas y ajustes
- T5.3 Documentación final

## Riesgos y recomendaciones

1. Hardware: si no tienes LiDAR, usa un sensor ultrasonido o define el proyecto como propuesta técnica.
2. Software: si no puedes instalar ROS2, documenta la arquitectura y ofrece pseudocódigo.
3. Tiempo: usa este plan para priorizar primero el chasis, la comunicación y la navegación.

## Qué hacer ahora

- Si tu entrega es escrita, usa estos dos archivos como base.
- Si necesitas un informe más corto, dime y te preparo un resumen ejecutivo.
- Si quieres, también puedo ayudarte a crear pseudocódigo para la parte de control o un diagrama de nodos.
