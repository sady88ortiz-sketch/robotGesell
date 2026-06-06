# Gantt, Grafo de Precedencias y Camino Crítico

## Introducción

La planificación del proyecto permite organizar las actividades necesarias para el desarrollo del vehículo autónomo subacuático de limpieza de piscinas (AquaCleanBot), identificando dependencias, tiempos de ejecución, riesgos y actividades críticas.

---

## Tabla de Actividades

| ID | Actividad | Duración (días) | Dependencia |
|----|-----------|----------------|-------------|
| AN-01 | Definición de requisitos | 3 | - |
| AN-02 | Investigación tecnológica | 4 | AN-01 |
| DS-01 | Diseño mecánico del casco | 5 | AN-02 |
| DS-02 | Diseño electrónico | 4 | AN-02 |
| AD-01 | Selección y adquisición de componentes | 3 | DS-01, DS-02 |
| CN-01 | Construcción del prototipo | 7 | AD-01 |
| SW-01 | Desarrollo de software de navegación | 8 | DS-02 |
| IN-01 | Integración hardware y software | 5 | CN-01, SW-01 |
| TS-01 | Pruebas de navegación | 4 | IN-01 |
| TS-02 | Pruebas de limpieza y recolección | 3 | TS-01 |
| CR-01 | Corrección y optimización | 3 | TS-02 |
| DOC-01 | Elaboración de documentación final | 2 | CR-01 |

---

## Grafo de Precedencias

```text
AN-01 Definición de requisitos
          │
          ▼
AN-02 Investigación tecnológica
          │
          ▼
     ┌─────────────┐
     │             │
     ▼             ▼
DS-01         DS-02
Diseño        Diseño
Mecánico    Electrónico
     │             │
     └──────┬──────┘
            ▼
AD-01 Selección de Componentes
            │
            ▼
CN-01 Construcción del Prototipo
            │
            │
DS-02 ──► SW-01 Desarrollo Software
            │
            ▼
IN-01 Integración
            │
            ▼
TS-01 Pruebas de Navegación
            │
            ▼
TS-02 Pruebas de Limpieza
            │
            ▼
CR-01 Correcciones
            │
            ▼
DOC-01 Documentación Final
```

---

## Camino Crítico

El camino crítico corresponde a la secuencia de actividades que determina la duración mínima total del proyecto.

```text
AN-01 → AN-02 → DS-01 → AD-01 → CN-01 → IN-01 → TS-01 → TS-02 → CR-01 → DOC-01
```

Duración estimada total: **39 días de trabajo.**

Cualquier retraso en estas actividades impactará directamente en la fecha final de entrega.

---

## Identificación de Cuellos de Botella

### Construcción del Prototipo (CN-01)

La fabricación e impermeabilización del casco representan una etapa crítica debido a los requerimientos de estanqueidad y seguridad eléctrica.

### Desarrollo de Software (SW-01)

La implementación de algoritmos de navegación autónoma y evasión de obstáculos requiere validación continua y pruebas iterativas.

### Integración Hardware-Software (IN-01)

Es la fase con mayor complejidad técnica, ya que deben funcionar correctamente sensores, motores, controladores y algoritmos de navegación.

---

## Riesgos del Proyecto

- Ingreso de agua al compartimiento electrónico.
- Fallas de sensores durante la navegación.
- Pérdida de estabilidad del vehículo.
- Consumo excesivo de energía.
- Retrasos en la adquisición de componentes.

---

## Estrategias de Mitigación

- Realizar pruebas de estanqueidad previas a la integración.
- Utilizar sellado impermeable en todos los compartimientos electrónicos.
- Implementar monitoreo permanente del nivel de batería.
- Realizar pruebas progresivas antes de la validación final.
- Mantener componentes de reemplazo disponibles para contingencias.

---

## Cronograma General

| Actividad | Inicio | Fin |
|------------|---------|---------|
| Definición de requisitos | Día 1 | Día 3 |
| Investigación tecnológica | Día 4 | Día 7 |
| Diseño mecánico | Día 8 | Día 12 |
| Diseño electrónico | Día 8 | Día 11 |
| Selección de componentes | Día 13 | Día 15 |
| Construcción del prototipo | Día 16 | Día 22 |
| Desarrollo de software | Día 12 | Día 19 |
| Integración | Día 23 | Día 27 |
| Pruebas de navegación | Día 28 | Día 31 |
| Pruebas de limpieza | Día 32 | Día 34 |
| Correcciones | Día 35 | Día 37 |
| Documentación final | Día 38 | Día 39 | 
