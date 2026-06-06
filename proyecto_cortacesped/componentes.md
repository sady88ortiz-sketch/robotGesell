# Componentes del Proyecto

Este documento define los componentes recomendados para el proyecto y sus alternativas.

## 1. Hardware principal

- **Chasis**
  - Placa de aluminio o acrílico resistente.
  - Alternativa: plataforma de robot comercial pequeña.
- **Motores de tracción**
  - Motores DC con reductora 12V.
  - Alternativa: motores paso a paso con control de velocidad.
- **Controladores de motores**
  - BTS7960 o MDD10A para motores DC.
  - Alternativa: puente H L298N para proyectos más económicos.
- **Batería**
  - Pack LiFePO4 12V o 24V con BMS.
  - Alternativa: batería de plomo sellada 12V si no hay LiFePO4.

## 2. Sensores

- **LiDAR 2D**
  - RPLiDAR A1/A2 para mapeo y navegación.
  - Alternativa: sensores ultrasónicos (más básico) o LiDAR de bajo costo.
- **Cámara RGB**
  - Cámara USB o Raspberry Pi Camera Module.
  - Alternativa: cámara móvil del teléfono para pruebas de visión.
- **IMU**
  - MPU6050/MPU9250 para orientación y fusión de sensores.
  - Alternativa: solamente encoders si el presupuesto es limitado.
- **Encoders**
  - Encoders de cuadratura en las ruedas.
  - Alternativa: usar estimación de distancia en los motores si no hay encoders.

## 3. Computación

- **SBC**
  - Raspberry Pi 4 (4GB/8GB) o NVIDIA Jetson Nano.
  - Alternativa: computadora pequeña con Linux capaz de ejecutar ROS 2.
- **MCU**
  - ESP32 para control de motores y seguridad.
  - Alternativa: Arduino Nano con comunicación serial.

## 4. Software y librerías

- **Sistema operativo**
  - Ubuntu 22.04 o Raspberry Pi OS con ROS 2 Humble/Foxy.
- **ROS 2**
  - `rclcpp`/`rclpy`, `nav2`, `slam_toolbox`, `robot_localization`, `teleop_twist_keyboard`.
- **Visión**
  - OpenCV, ONNX Runtime o TensorFlow Lite.
- **Comunicación**
  - micro-ROS sobre serial o MQTT local.

## 5. Seguridad y E-Stop

- **Botón físico de parada de emergencia**
  - Interruptor E-Stop en el chasis.
- **Parada de software**
  - Nodo ROS que publica estado de seguridad y detiene motores.

## Recomendaciones

- Si no puedes adquirir LiDAR, define el proyecto como una propuesta técnica con simulación.
- Prioriza componentes básicos que ya tengas: ruedas, motor DC, microcontrolador y una cámara simple.
- Usa alternativas más económicas solo si estás seguro de que podrás explicar su impacto en el proyecto.
