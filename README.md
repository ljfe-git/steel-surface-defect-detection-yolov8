<img width="600" height="600" alt="demo_inspeccion_acero (1)" src="https://github.com/user-attachments/assets/40d1e5ac-4789-4945-98aa-ae73d348c27c" />
# 🏭 SmartInspect-Industrial-CV: Detección y Tracking de Defectos en Tiempo Real

Sistema de Visión Artificial diseñado para entornos industriales (Industria 4.0). Este proyecto simula un pipeline de producción para la inspección de calidad en superficies de acero laminado sobre cintas transportadoras, integrando modelos de Deep Learning con lógicas de negocio reales.


## 🚀 Características Clave (Business Value)

Este repositorio va más allá de una inferencia estática tradicional, presentando una arquitectura lista para producción:

*   **Object Tracking (BoT-SORT):** Implementación de seguimiento de objetos en vídeo para asignar un **ID único** a cada defecto físico, evitando el conteo duplicado mientras la pieza atraviesa el campo de visión de la cámara.
*   **Doble Umbral de Seguridad (Human-in-the-Loop):** 
    *   *Umbral Visual (30%):* Muestra alertas preventivas en la pantalla del operario para supervisión manual de anomalías sospechosas.
    *   *Umbral de Acción (60%):* Registra automáticamente el defecto en la base de datos oficial solo cuando la certeza es alta, reduciendo falsas alarmas que detendrían innecesariamente la línea de producción.
*   **Logging Automático (CSV):** Generación de reportes tabulares en tiempo real (Fecha, Hora, Tipo de Defecto, Confianza, Fotograma e ID) listos para su integración con sistemas ERP/MES de la fábrica.
*   **Hardware Agnostic (ONNX):** Exportación automatizada del modelo YOLOv8 a formato **ONNX**. Esto elimina la dependencia de PyTorch/Python y permite una inferencia de ultra-baja latencia en PLCs o IPCs de planta usando C++ o C#.

![Demostración del sistema](demo_inspeccion_acero.gif)

## 📁 Estructura del Proyecto

El proyecto aplica el principio de *Separación de Responsabilidades*, dividiéndose en dos flujos de trabajo principales:

1.  `01_Entrenamiento_y_Datos.ipynb`: Cuaderno encargado del entrenamiento del modelo YOLOv8n sobre el dataset NEU-DET. Incluye además un script generador de datos sintéticos que crea un vídeo de la "cinta transportadora" a partir de imágenes estáticas de validación.
2.  `02_Inferencia_Video_Industrial.ipynb`: Cuaderno de producción. Recibe el flujo de vídeo, aplica el Object Tracking, calcula los FPS en tiempo real, genera el registro CSV, exporta el modelo a ONNX.
3.  `requirements.txt`: Dependencias necesarias para ejecutar el pipeline.

## 🛠️ Stack Tecnológico

*   **Modelo de Visión:** YOLOv8 (Ultralytics)
*   **Dataset:** NEU-DET (Steel Surface Defect Database) - Detecta 6 clases: *crazing, inclusion, patches, pitted_surface, rolled-in_scale, scratches*.
*   **Procesamiento de Vídeo:** OpenCV, Imageio, FFmpeg
*   **Exportación Industrial:** ONNX

## ⚙️ Uso y Despliegue

1. Clona este repositorio:
   ```bash
   git clone [https://github.com/TU_USUARIO/SmartInspect-Industrial-CV.git](https://github.com/TU_USUARIO/SmartInspect-Industrial-CV.git)
   cd SmartInspect-Industrial-CV
