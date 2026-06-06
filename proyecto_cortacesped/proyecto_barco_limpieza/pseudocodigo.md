# Pseudocódigo del Sistema

## Objetivo

Describir la lógica de funcionamiento del vehículo autónomo subacuático AquaCleanBot para la navegación, detección de obstáculos y limpieza de piscinas.

---

## Variables Principales

- nivelBateria
- distanciaObstaculo
- estadoLimpieza
- velocidadMotor
- posicionActual

---

## Pseudocódigo General

```text
INICIO

Inicializar sensores
Inicializar motores
Inicializar sistema de limpieza
Inicializar monitoreo de batería

Mientras nivelBateria > 20%

    Leer sensores

    Obtener distanciaObstaculo

    Si distanciaObstaculo < distanciaSegura Entonces

        Detener avance

        Girar 90 grados

        Continuar navegación

    Sino

        Avanzar

    Fin Si

    Activar sistema de limpieza

    Recolectar residuos

    Actualizar posicionActual

    Verificar nivelBateria

Fin Mientras

Detener motores

Desactivar sistema de limpieza

Generar reporte de operación

FIN
```

---

## Flujo Operativo

1. Inicialización de sistemas.
2. Verificación del nivel de batería.
3. Inicio de navegación autónoma.
4. Detección de obstáculos.
5. Corrección de trayectoria.
6. Activación del sistema de limpieza.
7. Recolección de residuos.
8. Monitoreo continuo de sensores.
9. Finalización de operación.
10. Generación de reporte.

---

## Funciones Principales

### Navegar()

```text
Leer sensores

Si existe obstáculo

    Cambiar dirección

Sino

    Continuar avance

Fin Si
```

### Limpiar()

```text
Activar turbina

Recolectar residuos

Almacenar residuos en depósito
```

### VerificarBateria()

```text
Si batería < 20%

    Regresar a punto de extracción

Fin Si
```

---

## Mejoras Futuras

- Navegación mediante inteligencia artificial.
- Mapeo automático de piscinas.
- Sistema de retorno automático.
- Estación de carga autónoma.
- Monitoreo remoto mediante aplicación móvil. 
