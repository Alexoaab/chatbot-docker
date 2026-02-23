
Chatbot con Python, Tkinter y Docker

⸻

Descripción del proyecto

Este proyecto consiste en el desarrollo de un chatbot en Python que utiliza la librería Tkinter para la creación de una interfaz gráfica de usuario y un archivo JSON como base de datos para almacenar preguntas y respuestas.

El chatbot permite al usuario introducir preguntas y obtener respuestas simples basadas en coincidencias de palabras clave. Además, puede proporcionar enlaces adicionales para ampliar la información.

El objetivo del proyecto es aplicar conceptos de desarrollo de aplicaciones, control de versiones con Git y GitHub, contenerización con Docker y orquestación con Docker Compose.

⸻

Instalación y despliegue

1. Clonar el repositorio
git clone https://github.com/Alexoaab/chatbot-docker.git
cd chatbot-docker
2. Construir la imagen Docker
docker build -t chatbot .
Este comando construye la imagen del contenedor a partir del Dockerfile.
3. Ejecutar el contenedor (modo gráfico)
Antes de ejecutar el contenedor, es necesario permitir el acceso al servidor gráfico:
xhost +local:docker
A continuación, ejecutar:
docker run --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix chatbot
Este comando permite que la aplicación gráfica se muestre en el sistema host.
4. Ejecutar con Docker Compose
docker compose up --build
Este comando construye y ejecuta el servicio definido en el archivo docker-compose.yml.
5. Acceso a la aplicación
La aplicación es de tipo gráfico (Tkinter), por lo que no se accede mediante navegador web ni URL.

La interfaz del chatbot se muestra directamente como una ventana en el sistema operativo.

plicación del Dockerfile

El archivo Dockerfile define la imagen del contenedor y contiene las siguientes acciones:
	•	Utiliza como base la imagen python:3.11-slim.
	•	Instala la librería tkinter, necesaria para la interfaz gráfica.
	•	Establece el directorio de trabajo dentro del contenedor.
	•	Copia los archivos de la aplicación (app.py y base_datos.json).
	•	Ejecuta automáticamente la aplicación al iniciar el contenedor.

⸻

Explicación del docker-compose.yml

El archivo docker-compose.yml permite gestionar el contenedor de forma más sencilla:
	•	Define un servicio llamado chatbot.
	•	Construye la imagen desde el Dockerfile.
	•	Configura un volumen para mantener la persistencia del archivo base_datos.json.
	•	Permite el uso de la interfaz gráfica mediante la variable de entorno DISPLAY.
	•	Comparte el socket del servidor gráfico (/tmp/.X11-unix) con el contenedor.
	•	Mantiene el contenedor en modo interactivo.
