# 🤖 Guía de Despliegue y Estructura del Bot

Este instructivo contiene los pasos exactos para configurar y subir este bot a Render (Plan Gratuito) usando las dependencias correctas.

---

## 📂 Archivos en tu Computadora (Estructura en la Raíz)
Asegúrate de que los siguientes 4 archivos estén guardados juntos en la misma carpeta antes de subirlos a tu repositorio:
1. `config.py` (Donde configuras los tokens y datos de cada bot)
2. `main.py` (El código principal del bot conectado a config.py)
3. `requirements.txt` (Las librerías necesarias para el servidor)
4. `INSTRUCCIONES.md` (Este manual de notas)

---

## 📦 Contenido Requerido en `requirements.txt`
Para que Render no lance errores de librerías faltantes, tu archivo debe contener exactamente:
```text
highrise-bot-sdk==25.1.0
flask
```

---

## 🚀 Pasos para Desplegar en Render (Web Service)

Al crear el nuevo **Web Service** en tu panel de Render, rellena los campos del formulario exactamente con estos datos:

* 📦 **Build Command:**  
  ```bash
  pip install -r requirements.txt
  ```

* 🚀 **Start Command:**  
  ```bash
  python main.py
  ```

* 🔑 **Environment Variables (Variables de Entorno):**  
  Busca el botón de añadir variable y pon:
  * **Key (Clave):** `PYTHON_VERSION`
  * **Value (Valor):** `3.11.0`

---

## ⏱️ Mantener el Bot Activo 24/7 con UptimeRobot

Render apaga las aplicaciones gratuitas si pasan 15 minutos sin recibir visitas. Para evitar que el bot se salga de la sala:

1. Copia la dirección web (URL) que te genera Render al terminar el despliegue (ejemplo: `https://onrender.com`).
2. Entra en tu panel de **UptimeRobot** o tu sistema de Cron Job preferido.
3. Crea un monitor nuevo configurado como tipo **HTTP(s)**.
4. Pega la URL de Render y pon el intervalo de alertas para que haga un ping **cada 5 o 10 minutos**.
5. Esto enviará una señal constante al servidor Flask en tu código, manteniendo el proceso despierto de forma ininterrumpida.
