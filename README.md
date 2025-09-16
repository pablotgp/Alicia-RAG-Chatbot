#  Cheshire: Una IA Conversacional Experta en "Alicia en el País de las Maravillas" 🐱

¡Bienvenido! Este proyecto es una inmersión profunda en la creación de una IA experta y con personalidad, utilizando una arquitectura RAG (Retrieval-Augmented Generation) de principio a fin. El resultado es un chatbot con el que puedes conversar sobre "Alicia en el País de las Maravillas" en dos modos: como un Asistente Factual o como el enigmático Gato de Cheshire.

---

## 🎯 Motivación

El objetivo era construir un sistema RAG robusto, diseñado a medida para un texto literario complejo, que fuera capaz de:
1.  **Responder preguntas con alta precisión**, basándose únicamente en el contenido del libro.
2.  **Evitar las "alucinaciones"** o invención de información, un problema común en los LLMs.
3.  **Adoptar una personalidad creativa y consistente** sin sacrificar la veracidad de los datos.

## 🛠️ Arquitectura y Stack Tecnológico

El sistema sigue un pipeline completo desde el PDF hasta la interfaz interactiva, todo contenido dentro de un único notebook para facilitar su ejecución.

1.  **Procesamiento de Datos:**
    - Limpieza automática de un PDF del libro.
    - **Chunking semántico y jerárquico** que respeta la estructura de capítulos.
    - Generación de embeddings con los modelos de **OpenAI**.
    - Creación de un índice vectorial en memoria con **FAISS**.

2.  **Pipeline de RAG:**
    - **Búsqueda Híbrida:** Combina la búsqueda vectorial (FAISS) con la búsqueda por palabras clave (**BM25**). Un sistema de pesos dinámicos analiza la pregunta para optimizar la estrategia.
    - **Reranking de Precisión:** Un modelo **Cross-Encoder** (`sentence-transformers`) refina los resultados para asegurar la máxima relevancia.
    - **Generación:** Se utiliza **Gemini 1.5 Flash** de Google AI, guiado por un sistema de **Prompt Engineering avanzado** para adoptar las personalidades.
    - **Interfaz:** Una aplicación web interactiva construida con **Gradio**.

### 🚀 Stack Principal
- **Lenguaje:** Python
- **LLM:** Google Gemini 1.5 Flash
- **Embeddings:** OpenAI `text-embedding-3-small`
- **Búsqueda Vectorial:** FAISS
- **Búsqueda por Palabras Clave:** `rank-bm25`
- **Reranking:** `sentence-transformers`
- **Framework de Orquestación:** LangChain
- **Interfaz:** Gradio

---

## 🚀 Cómo Ejecutarlo (Método Sencillo con Google Colab)

Este notebook está diseñado para ser ejecutado de principio a fin en un único entorno de Google Colab.

**1. Prepara tus Archivos:**
   - Clona o descarga este repositorio.
   - Crea un archivo `.env` a partir de la plantilla `.env.example` y pega tus claves de API de OpenAI y Google AI Studio.

**2. Abre el Notebook en Colab:**
   - Ve a [Google Colab](https://colab.research.google.com/) y selecciona `Archivo` > `Subir notebook`.
   - Sube el archivo `Alicia_Chatbot.ipynb`.

**3. Sube los Archivos del Proyecto a tu Sesión de Colab:**
   - Una vez abierto el notebook, haz clic en el icono de la carpeta (📁) en la barra lateral izquierda para abrir el panel de archivos.
   - Arrastra y suelta los siguientes archivos y carpetas desde tu ordenador a este panel:
     - El archivo PDF del libro (`119-2014-02-19-Carroll.AliciaEnElPaisDeLasMaravillas (1).pdf`).
     - Tu archivo `.env` con las claves.
     - La carpeta `assets` completa con las imágenes.

**4. ¡Ejecuta y Disfruta!**
   - Ejecuta todas las celdas del notebook en orden (`Entorno de ejecución` > `Ejecutar todo`).
   - Las primeras celdas instalarán las librerías y procesarán el PDF para crear los índices en memoria.
   - La última celda lanzará la interfaz de Gradio directamente en la salida.
   - **Recuerda:** La **primera pregunta** que hagas será más lenta mientras se inicializan todos los modelos.

## 🔮 Próximos Pasos

El siguiente desafío es evolucionar esta arquitectura monolítica en una **plataforma modular y escalable**, separando el pre-procesamiento de la aplicación principal para poder tomar *cualquier* libro y convertirlo en una base de conocimiento conversacional.
