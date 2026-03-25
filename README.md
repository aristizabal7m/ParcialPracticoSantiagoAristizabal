# Proyecto: FastAPI + Google Gemini (Gemini API)

Descripción
-----------
API sencilla construida con FastAPI que actúa como pasarela hacia la API de Google Gemini (cliente genai). Expone un endpoint REST que recibe un prompt y devuelve la respuesta generada por el modelo.

Características
---------------
- Endpoint: `GET /llm/{prompt}` — redirige el texto a Google Gemini y devuelve la respuesta.
- Basado en `FastAPI` y el cliente `genai` de Google (Gemini).

Requisitos
----------
- Python 3.10+ recomendado
- Dependencias principales (añadir a `requirements.txt` o instalar con `pip`):
	- fastapi
	- uvicorn
	- python-dotenv
	- google-genai (o el SDK oficial de Google para Gemini / genai)

Nota: en este repositorio puede haber un `requirements.txt` con paquetes del entorno; asegúrate de incluir al menos las dependencias listadas arriba para ejecutar esta aplicación.

Instalación
-----------
1. Clona el repositorio o descarga los archivos.
2. Crea y activa un entorno virtual (opcional pero recomendado):

```bash
python -m venv .venv
source .venv/bin/activate
```

3. Instala dependencias:

```bash
pip install -r requirements.txt
# o instalar individualmente
pip install fastapi uvicorn python-dotenv google-genai
```

Configuración (.env)
---------------------
La aplicación lee la variable de entorno `GEMINI_API_KEY` para autenticar con la API de Gemini. Crea un archivo `.env` en la raíz del proyecto con el siguiente contenido:

```
GEMINI_API_KEY=tu_api_key_de_gemini_aqui
```

Uso
---
1. Ejecuta la aplicación con Uvicorn (desde la raíz del proyecto):

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

2. Endpoint principal

- `GET /llm/{prompt}`

Descripción: envía el `prompt` al cliente de Gemini y devuelve la respuesta en JSON. En `main.py` la ruta devuelve un objeto con la clave `Respuesta` y el texto recibido del modelo.

Ejemplo de solicitud (curl)
--------------------------
```bash
curl -s "http://localhost:8000/llm/¿Cuál%20es%20la%20capital%20de%20Francia?"
```

Ejemplo de respuesta (JSON)
--------------------------
```json
{"Respuesta": "París."}
```

Notas de implementación
-----------------------
- El cliente se inicializa con `from google import genai` y crea `genai.Client()` esperando que la API key esté presente en la variable `GEMINI_API_KEY`.
- `main.py` contiene la lógica mínima para generar el contenido con `client.models.generate_content(...)`.

Buenas prácticas
---------------
- No expongas tu `GEMINI_API_KEY` en repositorios públicos.
- Considera agregar límites, caching y control de uso para evitar costes inesperados.

Soporte y contribución
----------------------
Si deseas mejorar el proyecto, crea un fork y envía un pull request con descripciones claras de los cambios.

Licencia
--------
Indica aquí la licencia del proyecto si aplica.

