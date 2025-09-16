#  Cheshire: Una IA Conversacional Experta en "Alicia en el País de las Maravillas"

¡Bienvenido! Este proyecto es una inmersión profunda en la creación de una IA experta y con personalidad, utilizando una arquitectura RAG (Retrieval-Augmented Generation) de principio a fin. El resultado es un chatbot con el que puedes conversar sobre "Alicia en el País de las Maravillas" en dos modos: como un Asistente Factual o como el enigmático Gato de Cheshire.


## 🎯 Motivación

El objetivo era construir un sistema RAG robusto, diseñado a medida para un texto literario complejo, que fuera capaz de:
1.  Responder preguntas con alta precisión, basándose únicamente en el contenido del libro.
2.  Evitar las "alucinaciones" o invención de información.
3.  Adoptar una personalidad creativa y consistente sin sacrificar la veracidad.

## 🛠️ Arquitectura y Stack Tecnológico

El sistema sigue un pipeline completo desde el PDF hasta la interfaz interactiva:

1.  **Procesamiento de Datos (`data_processing.ipynb`):**
    - Limpieza automática de un PDF del libro.
    - Chunking semántico y jerárquico que respeta la estructura de capítulos.
    - Generación de embeddings con los modelos de OpenAI.
    - Creación de un índice vectorial con FAISS.

2.  **Pipeline de RAG (`app.ipynb`):**
    - **Búsqueda Híbrida:** Combina la búsqueda vectorial (FAISS) con la búsqueda por palabras clave (BM25). Un sistema de pesos dinámicos analiza la pregunta para optimizar la estrategia de búsqueda.
    - **Reranking:** Un modelo Cross-Encoder refina los resultados para asegurar la máxima relevancia.
    - **Generación:** Se utiliza Gemini 1.5 Flash de Google AI, guiado por un sistema de Prompt Engineering avanzado para adoptar las personalidades.
    - **Interfaz:** Una aplicación web interactiva con pestañas y dos historiales de chat separados, construida con Gradio.

### 🚀 Stack Principal
- **Lenguaje:** Python
- **LLM:** Google Gemini 1.5 Flash
- **Embeddings:** OpenAI `text-embedding-3-small`
- **Búsqueda Vectorial:** FAISS
- **Búsqueda por Palabras Clave:** `rank-bm25`
- **Reranking:** `sentence-transformers` (Cross-Encoder)
- **Framework de Orquestación:** LangChain
- **Interfaz:** Gradio

## 🚀 Cómo Ejecutarlo

1.  **Clona el repositorio:**
    ```bash
    git clone https://github.com/tu-usuario/Alicia-RAG-Chatbot.git
    cd Alicia-RAG-Chatbot
    ```
2.  **Instala las dependencias:**
    ```bash
    pip install -r requirements.txt
    ```
3.  **Configura tus claves de API:**
    - Renombra el archivo `.env.example` a `.env`.
    - Abre `.env` y pega tus claves de API de OpenAI y Google AI Studio.

4.  **Genera los datos:**
    - Abre y ejecuta todas las celdas del notebook `data_processing.ipynb`. Esto procesará el PDF y creará los archivos `alicia.index`, `alicia_texts.pkl` y `alicia_metas.pkl`.

5.  **Lanza la aplicación:**
    - Abre y ejecuta todas las celdas del notebook `app.ipynb`. La interfaz de Gradio aparecerá en la salida de la última celda, ¡lista para usar!

## 🔮 Próximos Pasos

El siguiente desafío es evolucionar esta arquitectura a medida en una plataforma modular capaz de tomar *cualquier* libro y convertirlo en una base de conocimiento conversacional.