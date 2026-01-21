<div align="center">

# 🎤 Análisis de Voz — Transcripción Automática de Audios

![Status](https://img.shields.io/badge/status-ready-brightgreen.svg?style=for-the-badge)
![Python](https://img.shields.io/badge/python-3.7%2B-blue.svg?style=for-the-badge)
![FFmpeg](https://img.shields.io/badge/ffmpeg-required-orange.svg?style=for-the-badge)
![License](https://img.shields.io/badge/license-MIT-green.svg?style=for-the-badge)

**Transcripción inteligente de múltiples audios en español usando IA**

[⬇️ Instalación](#-instalación-rápida) • [📖 Uso](#-uso) • [⚙️ Configuración](#-configuración) • [🐛 Troubleshooting](#-solución-de-problemas)

</div>

---

## 📋 Tabla de contenidos

- [Acerca de](#-acerca-de)
- [Características](#-características)
- [Requisitos del sistema](#-requisitos-del-sistema)
- [Instalación rápida](#-instalación-rápida)
- [Guía de uso](#-uso)
- [Ejemplo de ejecución](#-ejemplo-de-ejecución)
- [Configuración avanzada](#-configuración)
- [Estructura del código](#-estructura-del-código)
- [Solución de problemas](#-solución-de-problemas)
- [Contribuir](#-contribuir)

---

## 🎯 Acerca de

**Análisis de Voz** es una herramienta de transcripción automática que convierte archivos de audio a texto usando **Faster-Whisper** (OpenAI Whisper optimizado) con soporte multiidioma e español. 

### ¿Qué hace?

1. 📁 **Lee una carpeta** completa de audios
2. 🔄 **Convierte automáticamente** cualquier formato a WAV mono PCM 16 kHz
3. 🤖 **Transcribe cada audio** usando IA en español
4. 📄 **Genera un documento Word** con todas las transcripciones
5. ⏱️ **Calcula ETA** en tiempo real mientras procesa

### Casos de uso

- 🎙️ Transcripción de entrevistas y podcasts
- 📹 Conversión de grabaciones de reuniones
- 📚 Archivado de contenido de audio
- 🔍 Análisis de contenido de voz
- 🎬 Subtitulado y documentación de videos

---

## ✨ Características

| Característica | Estado | Detalles |
|---|---|---|
| 🎵 **Múltiples formatos** | ✅ | MP3, WAV, GSM, AAC, MPEG, MPG, M4A, MP4 |
| 🔊 **Conversión automática** | ✅ | Convierte cualquier formato a WAV PCM 16 kHz |
| 📊 **Procesamiento por lotes** | ✅ | Procesa carpetas enteras de audios |
| 📈 **ETA en tiempo real** | ✅ | Muestra porcentaje y tiempo estimado |
| 📄 **Exportación Word** | ✅ | Genera `.docx` con transcripciones completas |
| 🎯 **Whisper (OpenAI)** | ✅ | Modelo de IA multiidioma, muy preciso |
| 🖥️ **Interfaz gráfica** | ✅ | Selección visual de carpeta sin línea de comandos |

---

## 📦 Requisitos del sistema

### Software requerido

| Componente | Versión | Notas |
|---|---|---|
| **Python** | 3.8+ | Necesario para ejecutar el script |
| **FFmpeg** | Última | Necesario para convertir audios |
| **CUDA** | Opcional | Para aceleración GPU (Nvidia) |

### Instalación por plataforma

<details>
<summary><b>🪟 Windows</b></summary>

```bash
# FFmpeg
# 1. Descargar desde: https://ffmpeg.org/download.html
# 2. Extraer en C:\ffmpeg
# 3. Añadir C:\ffmpeg\bin al PATH del sistema
# Verificar instalación:
ffmpeg -version
```

</details>

<details>
<summary><b>🐧 Linux (Ubuntu/Debian)</b></summary>

```bash
sudo apt-get update
sudo apt-get install ffmpeg
ffmpeg -version
```

</details>

<details>
<summary><b>🍎 macOS</b></summary>

```bash
brew install ffmpeg
ffmpeg -version
```

</details>

### Modelos Whisper

Faster-Whisper descarga automáticamente el modelo la primera vez que lo ejecutas. Disponibles:
- `tiny`: muy rápido, ~40MB (menor precisión)
- `base`: rápido, ~140MB (buena relación)
- `small`: recomendado, ~466MB (buena precisión)
- `medium`: ~1.5GB (muy preciso, más lento)
- `large`: ~2.9GB (máxima precisión, muy lento)

En el script (`analisis_de_voz.py`), modifica:
```python
WHISPER_MODEL_SIZE = "small"  # Cambia según tu hardware
```

---

## 🚀 Instalación rápida

### Paso 1: Clonar o descargar el proyecto

```bash
git clone https://github.com/tuusuario/analisis-de-voz.git
cd analisis-de-voz
```

### Paso 2: Crear entorno virtual

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/macOS
python -m venv venv
source venv/bin/activate
```

### Paso 3: Instalar dependencias Python

```bash
pip install -r requirements.txt
```

### Paso 4: Verificar configuración

```bash
python analisis_de_voz.py --check
# o simplemente:
python analisis_de_voz.py
```

✅ **¡Listo!** El script abrirá un diálogo para seleccionar la carpeta.

---

## 📖 Uso

### Ejecución básica

```bash
python analisis_de_voz.py
```

### Flujo de trabajo

1. **El script abre un diálogo** para elegir la carpeta con audios
2. **Carga el modelo Vosk** (una sola vez, en memoria)
3. **Para cada archivo:**
   - Convierte a WAV mono PCM 16 kHz
   - Transcribe usando IA
   - Guarda en documento Word
4. **Genera archivo `.docx`** con todas las transcripciones

### Archivo de salida

```
📁 carpeta_entrada/
├── audio1.mp3
├── audio2.wav
├── audio3.m4a
└── 2026-01-21_15-30-45_transcripcion.docx  ← AQUÍ
```

---

## 🖨️ Ejemplo de ejecución

```
🧠 Cargando modelo Whisper (small)...
✅ Modelo descargado y cargado en 8.5s

📊 1/3 | 33.3% | ETA 00:04:30 | Iniciando: entrevista.mp3
  📌 Duración del audio: 125.5 segundos
  ⏱️ Tiempo de transcripción: 42.3 segundos
  📝 Texto: "Buenas tardes, hoy hablaremos sobre inteligencia artificial..."
✅ Listo: entrevista.mp3 | 33.3% completado | ETA 00:02:45 | t=00:00:44

📊 2/3 | 66.6% | ETA 00:01:30 | Iniciando: reunión.wav
  📌 Duración del audio: 89.3 segundos
  ⏱️ Tiempo de transcripción: 31.7 segundos
  📝 Texto: "Acta de reunión del equipo de desarrollo..."
✅ Listo: reunión.wav | 66.6% completado | ETA 00:00:50 | t=00:00:33

📊 3/3 | 100.0% | ETA 00:00:00 | Iniciando: podcast.m4a
  📌 Duración del audio: 156.8 segundos
  ⏱️ Tiempo de transcripción: 48.2 segundos
  📝 Texto: "Episodio especial: tecnología en 2026..."
✅ Listo: podcast.m4a | 100.0% completado | ETA 00:00:00 | t=00:00:50

🏁 Terminado. Tiempo total: 00:02:27
✅ Transcripción guardada en: C:\ruta\carpeta\2026-01-21_15-30-45_transcripcion.docx
```

---

## ⚙️ Configuración

### Tamaño del modelo Whisper

En `analisis_de_voz.py`, línea 16:

```python
WHISPER_MODEL_SIZE = "small"  # Opciones: tiny, base, small, medium, large
```

- Más pequeño = más rápido pero menos preciso
- Más grande = más preciso pero más lento (requiere más RAM/GPU)

### Optimización de velocidad

En `analisis_de_voz.py`, línea 19:

```python
BEAM_SIZE = 2  # Más bajo => más rápido, menos preciso. Rango: 1-5
```

### Acelerar con GPU (CUDA)

En `analisis_de_voz.py`, línea 17:

```python
DEVICE = "cpu"  # Cambiar a "cuda" si tienes GPU Nvidia
COMPUTE_TYPE = "int8_float32"  # O "int8" para aún más velocidad
```

---

## 🏗️ Estructura del código

### Funciones principales

| Función | Propósito | Líneas |
|---|---|---|
| `seleccionar_carpeta()` | Abre diálogo para elegir carpeta | 27-31 |
| `convertir_a_wav()` | Convierte audio a WAV PCM 16 kHz | 33-54 |
| `transcribir_audio()` | Transcribe con Vosk | 56-101 |
| `cargar_modelo_vosk()` | Carga modelo en memoria | 103-112 |
| `analizar_carpeta()` | Orquesta el flujo completo | 114-191 |
| `fmt_hhmmss()` | Formatea segundos a HH:MM:SS | 11-17 |

### Flujo general

```
┌─────────────────────────────────────────┐
│ 1. Seleccionar carpeta                  │
└──────────────────┬──────────────────────┘
                   ↓
┌─────────────────────────────────────────┐
│ 2. Cargar modelo Vosk (una sola vez)    │
└──────────────────┬──────────────────────┘
                   ↓
┌─────────────────────────────────────────┐
│ 3. Para cada archivo de audio:          │
│    - Convertir a WAV                    │
│    - Transcribir con Vosk               │
│    - Guardar en Word                    │
└──────────────────┬──────────────────────┘
                   ↓
┌─────────────────────────────────────────┐
│ 4. Generar YYYY-MM-DD_transcripcion.docx│
└─────────────────────────────────────────┘
```

---

## 🐛 Solución de problemas

### ❌ "Modelo de Vosk no encontrado"

**Causa:** El modelo no está en la ruta configurada.

**Solución:**
1. Verifica que el modelo esté en `~/.vosk/models/es/`
2. Comprueba que la carpeta contenga los archivos del modelo
3. Si usas otra ruta, modifica `MODEL_PATH` en el script

```bash
# Verificar estructura en Windows
dir C:\Users\TuUsuario\.vosk\models\es
```

### ❌ "ffmpeg not found" o errores de conversión

**Causa:** FFmpeg no está instalado o no está en PATH.

**Solución:**
1. **Instalar FFmpeg** (ver sección [Requisitos](#-requisitos-del-sistema))
2. Verificar que esté en PATH:
   ```bash
   ffmpeg -version
   ```
3. Si sigue sin funcionar, reinicia la terminal

### ❌ "Audio demasiado corto"

**Causa:** El archivo de audio tiene menos de 1 segundo.

**Solución:** El script lo detecta automáticamente. Si quieres cambiar el límite, modifica `analisis_de_voz.py` línea 77.

### ❌ "Audio debe estar en formato mono WAV PCM 16-bit"

**Causa:** El WAV convertido no tiene el formato correcto.

**Solución:** Este error raramente ocurre; la herramienta convierte automáticamente. Si persiste:
1. Verifica que FFmpeg esté correctamente instalado
2. Intenta con otro archivo de audio

### ⚠️ El script es lento

**Soluciones:**
- La transcripción depende del hardware (CPU/RAM)
- Usa audios de mejor calidad (menos ruido)
- Procesa archivos en lotes pequeños si hay muchos

---

## 🤝 Contribuir

¿Quieres mejorar este proyecto?

1. **Haz un fork** del repositorio
2. **Crea una rama** para tu feature:
   ```bash
   git checkout -b feature/mi-mejora
   ```
3. **Commit y push:**
   ```bash
   git add .
   git commit -m "Añade mi mejora"
   git push origin feature/mi-mejora
   ```
4. **Abre un Pull Request** con descripción clara

---

## 📄 Licencia

Este proyecto está bajo licencia **MIT**. Puedes usarlo libremente en proyectos comerciales y personales.

---

<div align="center">

### ⭐ Si te fue útil, ¡dale una estrella!

**Preguntas o sugerencias:** Abre un [issue](https://github.com/tuusuario/analisis-de-voz/issues)

*Última actualización: 21 de enero de 2026*

</div>
