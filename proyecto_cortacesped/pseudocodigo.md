# Pseudocódigo para el Proyecto

Este documento contiene lógica simplificada para los módulos principales del robot.

## 1. Módulo de grabación (`Teach`)

```
Nodo Recorder:
  suscribirse a /pose
  suscribirse a /cmd_vel
  archivo = abrir('recorrido.json', modo='w')
  cada vez que llega una nueva pose:
    si el robot está en modo grabación:
      guardar timestamp, pose, cmd_vel en archivo
  al finalizar la grabación:
    cerrar archivo
```

## 2. Módulo de reproducción (`Repeat`)

```
Nodo Playback:
  recorrido = leer('recorrido.json')
  para cada punto en recorrido:
    pose_actual = esperar_publisher('/pose')
    error = calcular_error(pose_actual, punto.pose)
    comando = controlador_pure_pursuit(error)
    publicar('/cmd_vel', comando)
    esperar(0.1 segundos)
```

## 3. Control de E-Stop

```
Nodo Safety:
  suscribirse a /detections
  suscribirse a /estop_button
  cada vez que llega detección:
    si hay persona o animal dentro de zona crítica:
      publicar('/estop', true)
    sino:
      publicar('/estop', false)
  cada vez que llega botón E-Stop:
    si botón activado:
      publicar('/estop', true)
```

## 4. Comunicación SBC -> MCU

```
Nodo SerialBridge:
  abrir puerto serial '/dev/ttyUSB0', 115200
  cada 100 ms:
    mensaje = leer('/cmd_vel')
    paquete = formatear(Vx, Vy, YawRate, estop)
    enviar_serial(paquete)
    respuesta = leer_serial()
    parsear respuesta
    publicar('/battery', respuesta.voltage)
    publicar('/encoder', respuesta.encoders)
```

## 5. MCU: controlador de motores

```
Bucle principal en ESP32:
  inicializar motores, encoders, E-Stop
  leer serial mientras haya datos
  si paquete válido recibido:
    si estop == true: detener_motores()
    else: set_speed(left, right)
  actualizar encoders
  cada 50 ms:
    enviar_estado_serial(encoder_left, encoder_right, voltage)
```

## 6. Algoritmo de Pure Pursuit básico

```
funcion controlador_pure_pursuit(error):
  distancia = sqrt(error.x^2 + error.y^2)
  angulo_objetivo = atan2(error.y, error.x)
  yaw_error = angulo_objetivo - error.yaw
  velocidad_lineal = clamp(0.2 * distancia, 0, 0.4)
  velocidad_angular = clamp(1.0 * yaw_error, -1.0, 1.0)
  regresar (velocidad_lineal, velocidad_angular)
```

## 7. Ejemplo de formato de archivo de recorrido

```
[
  {"t": 0.0, "x": 0.0, "y": 0.0, "yaw": 0.0},
  {"t": 0.5, "x": 0.1, "y": 0.0, "yaw": 0.02},
  {"t": 1.0, "x": 0.2, "y": 0.0, "yaw": 0.03}
]
```

## 8. Recomendaciones

- Empieza probando el control manual y la grabación de la ruta.
- Luego agrega la reproducción y el controlador de seguimiento.
- Finalmente integra el E-Stop y la visión.
