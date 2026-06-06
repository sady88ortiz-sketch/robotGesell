# Arquitectura del Sistema

Este documento describe la arquitectura de hardware y software del robot cortacésped.

## 1. Visión general

El sistema se divide en dos capas principales:

- **Capa de alto nivel**: SBC ejecuta ROS 2, procesa sensores, mapea el entorno y genera comandos de navegación.
- **Capa de bajo nivel**: MCU controla los motores, lee encoders e implementa seguridad de E-Stop.

## 2. Bloques de hardware

1. **SBC (Raspberry Pi / Jetson)**
   - Ejecuta ROS 2 y nodos de navegación.
   - Procesa datos de LiDAR y cámara.
2. **MCU (ESP32)**
   - Controlador de motores y recepción de comandos `cmd_vel`.
   - Lectura de encoders y E-Stop físico.
3. **Sensores**
   - LiDAR 2D para mapeo y detección de obstáculos.
   - Cámara RGB para detección de personas y obstáculos dinámicos.
   - IMU + encoders para odometría.
4. **Actuadores**
   - Motores de tracción.
   - Motor de corte (opcional, controlado por relé/ESC).

## 3. Flujo de datos

1. La cámara envía imágenes a un nodo de visión.
2. El LiDAR envía escaneos al nodo SLAM.
3. El nodo de fusión de sensores genera odometría y pose.
4. El nodo de navegación recibe waypoints y genera comandos `cmd_vel`.
5. Los comandos de velocidad se envían al MCU por serial.
6. El MCU controla los motores y detiene el sistema si el E-Stop se activa.

## 4. Arquitectura de software ROS 2

### Nodos principales

- `teleop_node`
  - Permite manejar el robot manualmente para grabar un recorrido.
- `recorder_node`
  - Registra la secuencia de poses o waypoints mientras el robot es teleoperado.
- `slam_node`
  - Ejecuta `slam_toolbox` o `gmapping` para generar el mapa 2D.
- `localization_node`
  - Calcula la pose usando encoders, IMU y datos de sensor.
- `navigation_node`
  - Reproduce el recorrido y genera comandos de control.
- `vision_node`
  - Detecta personas y obstáculos en la cámara.
- `safety_node`
  - Publica el estado de E-Stop y seguridad.

### Tópicos ROS clave

- `/cmd_vel` — comandos de velocidad para el robot.
- `/odom` — odometría del robot.
- `/scan` — datos del LiDAR.
- `/map` — mapa 2D generado.
- `/pose` — pose estimada del robot.
- `/estop` — estado de parada de emergencia.
- `/detections` — objetos detectados por visión.

## 5. Comunicación entre SBC y MCU

- **Serial UART** — método recomendado.
- Formato mínimo del mensaje:
  - `Vx, Vy, YawRate, EStop`.
- El MCU responde con:
  - `encoder_left, encoder_right, battery_voltage, status`.

## 6. Seguridad y E-Stop

- Si el nodo `vision_node` detecta un humano/animal cercano, publica `/estop` activo.
- Si el botón físico se pulsa, el MCU corta la señal a los motores.
- El sistema debe detenerse inmediatamente ante pérdida de comunicación.

## 7. Modo de operación

1. **Grabación (Teach)**
   - El usuario mueve el robot con teleoperación.
   - El sistema guarda la trayectoria en un archivo.
2. **Reproducción (Repeat)**
   - El robot lee los waypoints guardados.
   - El nodo de navegación sigue la ruta automáticamente.
3. **Seguridad**
   - El E-Stop local y la detección por visión pueden detener el robot en cualquier momento.
