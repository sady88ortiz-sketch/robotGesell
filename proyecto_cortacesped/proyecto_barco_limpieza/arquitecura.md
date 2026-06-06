# Desarrollo de vehículo Autónomo subacuatico para limpieza de piscinas (AquaCleanBot)

## Introducción
La contaminación por residuos sólidos y la falta de monitoreo continuo en cuerpos de agua dulce (como lagos, lagunas y canales) representan un desafío ecológico crítico. Los métodos de limpieza tradicionales suelen ser costosos, lentos y conllevan riesgos para el personal humano.

Este proyecto propone el diseño, construcción e integración de un **Vehículo Autónomo de Superficie (USV - Unmanned Surface Vehicle)** acoplado a un sistema robótico de recolección de residuos superficiales. El sistema combina una arquitectura de hardware robusta y estanca con software avanzado basado en **ROS2**, permitiendo al navío ejecutar rutas de navegación autónoma mediante posicionamiento satelital (GPS), procesar imágenes en tiempo real para la detección de objetos flotantes y operar de manera segura mediante protocolos automáticos de mitigación de fallos (*failsafe*).

## Objetivos del Proyecto

### Objetivo General
Diseñar e integrar un prototipo funcional de barco autónomo capaz de navegar de forma autónoma en entornos acuáticos controlados y semi-controlados para realizar tareas de detección, recolección de residuos y monitoreo ambiental.

### Objetivos Específicos
*   **Hardware y Estanqueidad:** Diseñar un casco hidrodinámico estable y configurar un sistema de propulsión eléctrica y potencia aislado herméticamente frente a filtraciones de agua.
*   **Percepción y Localización:** Fusionar datos de sensores de navegación (GPS, Brújula digital e IMU) para estimar la orientación y posición precisa del vehículo en tiempo real.
*   **Visión Artificial:** Implementar un sistema de visión basado en cámaras de video y algoritmos de procesamiento de imágenes para la identificación selectiva de obstáculos y residuos flotantes.
*   **Navegación Autónoma:** Desarrollar un sistema de guiado automatizado por puntos de control (*waypoints*) e implementar algoritmos para la evasión dinámica de obstáculos fijos o móviles.
*   **Seguridad y Conectividad:** Establecer un enlace de telemetría robusto e integrar un módulo de parada de emergencia remota (*E-Stop*) junto con rutinas de retorno automático a base en caso de pérdida de señal.
*   **Validación Experimental:** Validar el comportamiento del sistema mediante un plan de pruebas progresivo que abarque desde simulaciones e integración en entornos controlados (piscina) hasta su despliegue final en un entorno real (lago o mar).

 
