# 🌿 Detección de Enfermedades en Plantas con YOLOv8

**Materia:** Visión Artificial  
**Integrantes:** Josue Gale Guzman Chavez
**Registro:** 23110129
**Dataset:** PlantDoc — 30 clases, 2,569 imágenes  
**Modelo:** YOLOv8n (Ultralytics)

---

## Descripción del Proyecto

Este proyecto implementa un modelo de detección de objetos basado en YOLOv8 entrenado con el dataset PlantDoc, capaz de identificar en imágenes de hojas si una planta se encuentra **saludable** o si presenta **indicios de enfermedad, plaga o mal cuidado**, clasificando el tipo de daño detectado en tiempo real.

El modelo fue entrenado con 30 clases que incluyen cultivos como tomate, manzana, uva, maíz, papa, entre otros, cubriendo tanto estados saludables como enfermedades comunes.

---

## Instrucciones para Correr el Código

### Requisitos previos
- Cuenta en [Google Colab](https://colab.research.google.com)
- Cuenta en [Roboflow](https://roboflow.com) (gratuita)

### Pasos

1. Abre el archivo `notebooks/Proyecto_Vision_Artificial.ipynb` en Google Colab
2. Ve a `Entorno de ejecución → Cambiar tipo de entorno de ejecución → GPU T4`
3. En la **Celda 4**, reemplaza `"TU_API_KEY_AQUI"` con tu API key personal de Roboflow
4. Ejecuta las celdas **una por una** en orden de arriba hacia abajo
5. El entrenamiento (Celda 5) tarda aproximadamente **20-25 minutos**
6. Al finalizar, las imágenes de detección se guardan automáticamente en `runs/detect/evidencias/`

### Dependencias
Todas las dependencias están en `requirements.txt`. Se instalan automáticamente en la Celda 1 del notebook.

```bash
pip install -r requirements.txt
```

---

## Caso de Estudio: Sistema de Monitoreo Automatizado en Invernadero

### Problema a Resolver

Los agricultores e ingenieros agrónomos que trabajan en invernaderos enfrentan el reto de monitorear cientos o miles de plantas de forma manual, lo cual es costoso en tiempo y mano de obra. Las enfermedades y plagas pueden propagarse rápidamente si no se detectan a tiempo, causando pérdidas significativas en la producción. El objetivo es automatizar este monitoreo mediante visión artificial para detectar de forma temprana cualquier anomalía en las plantas.

---

### Hardware Propuesto

#### Cámaras
- **Tipo:** Cámaras IP de alta resolución (Full HD 1080p), con lente gran angular
- **Modelo de referencia:** Hikvision DS-2CD2143G2-I o similar
- **Cantidad:** Una cámara cada 4-6 metros lineales de cultivo, cubriendo el follaje de las plantas desde arriba en un ángulo de 45°
- **Conectividad:** PoE (Power over Ethernet) para simplificar el cableado

#### Unidad de Procesamiento
- **Dispositivo principal:** NVIDIA Jetson Orin Nano — computadora embebida con GPU dedicada, diseñada para aplicaciones de IA en el borde (edge computing)
- **Alternativa económica:** Raspberry Pi 5 con cámara HQ Module para invernaderos pequeños
- **Función:** Recibir el video de las cámaras, correr el modelo YOLOv8 en tiempo real y generar alertas

#### Red y Conectividad
- **Red local:** Switch PoE conectado a todas las cámaras y a la unidad de procesamiento
- **Conexión a internet:** Router WiFi para enviar notificaciones al agricultor vía app o correo

#### Sistema de Notificaciones
- **Pantalla local:** Monitor en la oficina del invernadero mostrando el feed en vivo con las detecciones
- **App móvil / Telegram Bot:** Notificación automática al teléfono del agricultor cuando se detecta una enfermedad, indicando la cámara, la planta afectada y el tipo de daño

---

### Flujo de Funcionamiento

```
[Planta en invernadero]
        ↓
[Cámara IP captura imagen cada 5 segundos]
        ↓
[Imagen enviada por red local a Jetson Orin Nano]
        ↓
[Modelo YOLOv8 analiza la imagen]
        ↓
  ┌─────────────────────────────┐
  │  ¿Se detectó algún daño?    │
  └─────────────────────────────┘
        ↓ SÍ                ↓ NO
[Genera alerta]       [Continúa monitoreo]
        ↓
[Identifica tipo de daño:
 enfermedad, plaga o mal cuidado]
        ↓
[Envía notificación al agricultor:
 - Cámara donde se detectó
 - Tipo de daño detectado
 - Tratamiento recomendado]
        ↓
[Agricultor interviene con
 el tratamiento adecuado]
```

---

### Tipos de Daño Detectados y Tratamientos

| Tipo de Daño | Descripción | Tratamiento Recomendado |
|---|---|---|
| Tizón temprano (Early Blight) | Manchas oscuras en hojas de tomate o papa | Fungicida a base de cobre, eliminar hojas afectadas |
| Tizón tardío (Late Blight) | Lesiones acuosas en hojas, muy contagioso | Fungicida sistémico, aumentar ventilación |
| Oídio (Powdery Mildew) | Polvo blanco sobre las hojas | Azufre coloidal, reducir humedad |
| Mancha foliar | Círculos amarillos o cafés en las hojas | Fungicida preventivo, mejorar drenaje |
| Hoja saludable | Sin anomalías detectadas | Continuar cuidado regular |

---

### Ventajas del Sistema

- **Monitoreo 24/7** sin necesidad de personal permanente
- **Detección temprana** antes de que la enfermedad se propague
- **Reducción de pérdidas** en la producción del invernadero
- **Escalable** — se pueden agregar más cámaras conforme crece el invernadero
- **Bajo costo operativo** una vez instalado el sistema

---

## Evidencias

Las imágenes de detección con bounding boxes generadas por el modelo se encuentran en la carpeta `/evidencias`.

## Modelo Entrenado

El archivo `best.pt` con los pesos del modelo entrenado se encuentra en la carpeta `/modelo`.

---

*Proyecto desarrollado para la materia de Visión Artificial*
