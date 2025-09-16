#  Cheshire: Una IA Conversacional Experta en "Alicia en el País de las Maravillas" 🐱

¡Bienvenido! Este proyecto es una inmersión profunda en la creación de una IA experta y con personalidad, utilizando una arquitectura RAG (Retrieval-Augmented Generation) de principio a fin. El resultado es un chatbot con el que puedes conversar sobre "Alicia en el País de las Maravillas" en dos modos: como un Asistente Factual o como el enigmático Gato de Cheshire.

### ✨ Demo en Acción

![Demo del Chatbot de Alicia](assets/demo.gif)
*(Nota: La inicialización del sistema en la primera pregunta tarda aproximadamente un minuto. Las respuestas posteriores son mucho más rápidas.)*

---

## 🎯 Motivación

El objetivo era construir un sistema RAG robusto, diseñado a medida para un texto literario complejo, que fuera capaz de:
1.  **Responder preguntas con alta precisión**, basándose únicamente en el contenido del libro.
2.  **Evitar las "alucinaciones"** o invención de información, un problema común en los LLMs.
3.  **Adoptar una personalidad creativa y consistente** sin sacrificar la veracidad de los datos.

## 🛠️ Arquitectura y Stack Tecnológico

El sistema sigue un pipeline completo desde el PDF hasta la interfaz interactiva, todo contenido dentro de un único notebook para facilitar su ejecución.

**Pipeline "Todo en Uno" (`Alicia_Chatbot.ipynb`):**
1.  **Procesamiento de Datos:**
    - Limpieza automática de un PDF del libro.
    - **Chunking semántico y jerárquico** que respeta la estructura de capítulos.
    - Generación de embeddings con los modelos de **OpenAI**.
    - Creación de un índice vectorial en memoria con **FAISS**.
2.  **Pipeline de RAG:**
    - **Búsqueda Híbrida:** Combina la búsqueda vectorial (FAISS) con la búsqueda por palabras clave (**BM25**). Un sistema de pesos dinámicos analiza la pregunta para optimizar la estrategia.
    - **Reranking de Precisión:** Un modelo **Cross-Encoder** (`sentence-transformers`) refina los resultados para asegurar la máxima relevancia.
    - **Generación:** Se utiliza **Gemini 1.5 Flash** de Google AI, guiado por un sistema de **Prompt Engineering avanzado** para adoptar las personalidades.
3.  **Interfaz Interactiva:** Una aplicación web construida con **Gradio**.

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

## 🚀 Cómo Ejecutarlo (Método Recomendado: Google Drive + Colab)

Este método es el más robusto, ya que mantiene todos tus archivos organizados y persistentes en un solo lugar.

**1. Prepara tu Entorno en Google Drive:**
   - Clona o descarga este repositorio y sube la carpeta `Alicia-RAG-Chatbot` completa a la raíz de tu Google Drive.
   - Dentro de la carpeta del proyecto en Google Drive, renombra `.env.example` a `.env` y añade tus claves de API de OpenAI y Google AI Studio.

**2. Ejecuta el Notebook en Google Colab:**
   - Navega a la carpeta del proyecto en tu Google Drive y abre el notebook `Alicia_Chatbot.ipynb`.
   - Arrastra y suelta el archivo PDF del libro desde tu ordenador al panel de los archivos de google colab, de cualquir forma no olvides de modificar esta ruta para procesar el libro, en mi caso es:
     `pdf_path = "/content/119-2014-02-19-Carroll.AliciaEnElPaisDeLasMaravillas (1).pdf"`.
   - **¡Paso Crítico!** Ejecuta la **primera celda de código**. Esta celda **montará tu Google Drive**, dándole al notebook acceso a tu PDF, claves de API y assets. Deberás autorizar la conexión.
   - Una vez montado el Drive, ejecuta todas las celdas restantes (`Entorno de ejecución` > `Ejecutar todo`).

**3. ¡Disfruta de la Aplicación!**
   - El notebook procesará el libro, creará los índices y lanzará la interfaz de Gradio en la salida de la última celda.
   - **Recuerda:** La **primera pregunta** que hagas será más lenta mientras se inicializan todos los modelos en memoria.

## 🔮 Próximos Pasos

El siguiente desafío es evolucionar esta arquitectura a medida en una **plataforma modular y escalable**, separando el pre-procesamiento de la aplicación principal para poder tomar *cualquier* libro y convertirlo en una base de conocimiento conversacional e inteligente.
