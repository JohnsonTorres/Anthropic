# Anthropic Claude API - Curso

Repositorio de aprendizaje del curso de la API de Anthropic con Python.

## Requisitos

- Python 3.8+
- Cuenta en Anthropic con API key

## Instalación

```bash
pip install anthropic python-dotenv
```

Crea un archivo `.env` en la raíz del proyecto con tu API key:

```
ANTHROPIC_API_KEY=tu_api_key_aqui
```

## Contenido del curso

### 001 - Requests básicos y conversaciones multi-turno

Introducción al cliente de Anthropic y cómo construir conversaciones con historial de mensajes.

**Conceptos clave:**
- Inicializar el cliente `Anthropic()` cargando credenciales desde `.env`
- Estructura de mensajes: roles `user` y `assistant`
- Parámetro `max_tokens` para controlar la longitud de la respuesta
- Mantener el historial de conversación en una lista de mensajes para habilitar contexto multi-turno

```python
from anthropic import Anthropic
from dotenv import load_dotenv

load_dotenv()
client = Anthropic()

messages = []
messages.append({"role": "user", "content": "¿Qué es la computación cuántica?"})

response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=1000,
    messages=messages
)
```

### 002 - System Prompt

Cómo definir la personalidad, rol y restricciones del asistente usando el parámetro `system`.

**Conceptos clave:**
- El `system prompt` se pasa por separado al array de `messages`
- Permite definir comportamiento, tono y restricciones del modelo
- El mismo historial de conversación puede producir respuestas distintas según el system prompt

```python
system_prompt = """
You are a patient math tutor.
Do not directly answer a student's questions.
Guide them to a solution step by step.
"""

response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=1000,
    messages=messages,
    system=system_prompt
)
```

### 003 - Temperature

Control del nivel de creatividad y aleatoriedad en las respuestas del modelo.

**Conceptos clave:**
- `temperature=0.0`: respuestas deterministas y precisas, ideal para tareas analíticas o matemáticas
- `temperature=1.0`: respuestas más creativas y variadas (valor por defecto)
- Rango válido: `0.0` a `1.0`
- Se puede combinar con system prompt para ajustar tanto el rol como la creatividad

```python
# Respuesta determinista
response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=1000,
    messages=messages,
    temperature=0.0
)

# Respuesta creativa
response = client.messages.create(
    model="claude-sonnet-4-6",
    max_tokens=1000,
    messages=messages,
    temperature=1.0
)
```

## Modelo utilizado

`claude-sonnet-4-6` — modelo principal usado en todos los ejercicios del curso.
