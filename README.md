# Nodo Andino Ads — app Android (v0.1)

Reproductor de publicidad en modo kiosco para tablets en vehículos y locales comerciales.

## Obtener el APK
Cada vez que se sube un cambio a `main`, GitHub Actions compila la app.
Entrá a la pestaña **Actions** del repositorio, abrí la última ejecución de "Compilar APK" y descargá **NodoAndino-apk**.

## Instalar en la tablet
1. Copiá `NodoAndino-v0.1.apk` a la tablet.
2. Abrilo y aceptá "instalar apps de origen desconocido".
3. La app arranca sola al encender la tablet.

## Configurar el dispositivo
Tocá el logo **5 veces seguidas**. El PIN inicial es **2468** (cambialo en la misma pantalla).
Ahí se cargan el modo (vehículo / local), el nombre del conductor o local, el Wi-Fi, la localidad, la zona, las coordenadas para el clima y la URL del servidor.

## Servidor (para conectar con nodoandino.com)
Si el campo "Servidor" está vacío, la app muestra los anuncios de demo.
Con servidor configurado, la app usa:

- `GET {servidor}/api/paquete?dispositivo=ID&version=V` cada 10 min. Devuelve:
  ```json
  {"version":"12","licencia":{"activa":true},"anuncios":[
    {"id":"a1","kicker":"","titulo":"","texto":"","qrTexto":"","qr":"https://…png",
     "imagen":"https://…jpg","video":"https://…mp4","acento":"#E91EF5","segundos":15,
     "reglas":{"dias":[5,6],"desde":16,"hasta":20,"clima":["frio"],"localidades":["Bariloche"],"zonas":["Centro"],"tipo":"vehiculo"}}
  ]}
  ```
  Con `licencia.activa: false` la pantalla se bloquea.
- `POST {servidor}/api/exposicion` cada 5 min con los segundos mostrados por anuncio y por día, que sirven de base para la liquidación.

El clima viene de Open-Meteo (gratis, sin clave).
