# Proyecto: Cortadora de Pasto Semi-Autónoma

Este proyecto es una versión propia basada en el concepto del repositorio original. La idea es diseñar y documentar un sistema de robótica móvil que pueda aprender un recorrido guiado y reproducirlo con seguridad.

## Objetivo

Desarrollar un proyecto que incluya:
- diseño de hardware básico
- arquitectura de control (SBC + MCU)
- planificación de software para navegación y detección
- un plan de trabajo con tareas, dependencias y camino crítico

## Alcance de la tarea

Para un proyecto escolar puedes entregar:
- documentación técnica del sistema
- plan de trabajo y cronograma
- propuesta de componentes
- diagrama de flujo / arquitectura
- si tienes tiempo, una simulación simple o pseudocódigo de control

## Partes principales

1. Diseño de hardware
   - chasis, motores, batería, sensores
   - SBC (Raspberry Pi / Jetson) y MCU (ESP32)
2. Firmware de bajo nivel
   - control de motores, lectura de encoders
   - comunicación entre SBC y MCU
3. Software de alto nivel
   - ROS 2 básico o estructura de nodos
   - SLAM u odometría
   - navegación "teach-and-repeat"
4. Visión y seguridad
   - cámara, detección de obstáculos
   - E-Stop / parada de emergencia
5. Integración y pruebas
   - pruebas controladas en laboratorio
   - ajustes finales y documentación

## Documentos adicionales

- `planificacion.md`: contiene la planificación de tareas, el Gantt y el camino crítico.
- `componentes.md`: lista de componentes recomendados y alternativas.
- `arquitectura.md`: arquitectura de hardware/software y flujo de datos.
- `pseudocodigo.md`: pseudocódigo para grabación, reproducción, E-Stop y control.

## Cómo usar esta carpeta

1. Lee `planificacion.md` para entender el plan de trabajo.
2. Revisa `componentes.md` para elegir el hardware y los sensores.
3. Consulta `arquitectura.md` para ver el diseño del sistema.
4. Usa `pseudocodigo.md` si necesitas escribir código o explicarlo en el informe.

## Siguiente paso

1. Elige cuál de estas entregas necesitas:
   - informe técnico completo
   - presentación de proyecto
   - diagrama de bloques y pseudocódigo
   - propuesta simplificada si no tienes todos los componentes
2. Dime qué quieres que prepare ahora y lo hago.
