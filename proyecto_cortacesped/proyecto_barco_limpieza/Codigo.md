// Código Base para Robot Limpia Piscina (Arduino / ESP32)
const int ENA = 5;  // Velocidad Motor Izquierdo
const int IN1 = 4;  // Dirección 1
const int IN2 = 2;  // Dirección 2
const int ENB = 18; // Velocidad Motor Derecho
const int IN3 = 19; // Dirección 3
const int IN4 = 21; // Dirección 4

const int trigPin = 12;
const int echoPin = 14;

void setup() {
  pinMode(ENA, OUTPUT);
  pinMode(ENB, OUTPUT);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);
  pinMode(IN3, OUTPUT);
  pinMode(IN4, OUTPUT);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(115200);
}

void loop() {
  long duration;
  int distance;

  // Medir distancia con sensor ultrasónico (delante)
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
 
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  // Lógica de navegación básica: Si hay obstáculo cerca (< 20cm), gira; si no, avanza limpiando.
  if (distance < 20 && distance > 0) {
    // Obstáculo detectado: Girar para esquivar pared de la piscina
    girarDerecha();
    delay(1000);
  } else {
    // Camino libre: Avanzar hacia adelante
    avanzar(200); // Velocidad PWM 200
  }
}

void avanzar(int velocidad) {
  analogWrite(ENA, velocidad);
  analogWrite(ENB, velocidad);
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, HIGH);
  digitalWrite(IN4, LOW);
}

void girarDerecha() {
  analogWrite(ENA, 200);
  analogWrite(ENB, 200);
  digitalWrite(IN1, HIGH);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, HIGH);
}
